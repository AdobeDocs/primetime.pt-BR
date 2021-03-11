---
description: O TVSDK fornece geradores de oportunidades padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.
title: Geradores de oportunidades e resolvedores de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Geradores de oportunidades e resolvedores de conteúdo {#opportunity-generators-and-content-resolvers}

O TVSDK fornece geradores de oportunidades padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que geralmente indica uma oportunidade de posicionamento de anúncios. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo, como um período de blecaute. Um *`opportunity generator`* identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK de que essas oportunidades foram marcadas. As oportunidades são identificadas em uma linha do tempo no ao incluir uma tag não padrão (não HLS).

Quando seu aplicativo é notificado sobre uma oportunidade, seu aplicativo pode alterar a linha do tempo inserindo uma série de anúncios, alternando para um fluxo alternativo (blecautes) ou editando o conteúdo da linha do tempo. Por padrão, o TVSDK chama o *`content resolver`* apropriado para implementar as alterações ou ações necessárias da linha do tempo. Seu aplicativo pode usar o resolvedor de conteúdo de anúncio TVSDK padrão ou registrar seu próprio resolvedor de conteúdo.

Você também pode usar `MediaPlayerItemConfig.setAdTags` para adicionar mais marcadores de anúncio/dicas, de modo que o TVSDK possa reconhecer e usar `MediaPlayerItemConfig.subscribedTags` e notificar seu aplicativo sobre marcadores adicionais que possam ter informações de fluxo de trabalho de publicidade.

Um possível uso de um resolvedor personalizado é para períodos de blecaute. Para lidar com esses períodos, seu aplicativo pode implementar e registrar um detector de oportunidade de blecaute responsável por manipular tags de blecaute. Quando o TVSDK encontra essa tag, ele pesquisa todos os resolvedores de conteúdo registrados para localizar o primeiro que manipula a tag especificada. Neste exemplo, é o resolvedor de conteúdo do blackout, que pode, por exemplo, substituir o item atual por conteúdo alternativo no reprodutor pela duração especificada pela tag .