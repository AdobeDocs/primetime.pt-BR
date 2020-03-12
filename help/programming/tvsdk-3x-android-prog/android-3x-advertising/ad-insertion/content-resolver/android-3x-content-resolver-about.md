---
description: O TVSDK fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.
seo-description: O TVSDK fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.
seo-title: Geradores de oportunidade e resolvedores de conteúdo
title: Geradores de oportunidade e resolvedores de conteúdo
uuid: 5caf8924-3d76-45a1-a136-39932abe88b3
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Geradores de oportunidade e resolvedores de conteúdo {#opportunity-generators-and-content-resolvers}

O TVSDK fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto, como indicadores para um período de blecaute.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que geralmente indica uma oportunidade de colocação de anúncio. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo, como um período de blecaute. Um *`opportunity generator`* identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK de que essas oportunidades foram marcadas. As oportunidades são identificadas em uma linha do tempo ao incluir uma tag não padrão (não HLS).

Quando seu aplicativo é notificado sobre uma oportunidade, seu aplicativo pode alterar a linha do tempo inserindo uma série de anúncios, alternando para um fluxo alternativo (blecautes) ou editando o conteúdo da linha do tempo. Por padrão, o TVSDK chama o apropriado *`content resolver`* para implementar as alterações ou ações necessárias na linha do tempo. Seu aplicativo pode usar o resolvedor de conteúdo de anúncio TVSDK padrão ou registrar seu próprio resolvedor de conteúdo.

Você também pode usar `MediaPlayerItemConfig.setAdTags` para adicionar mais tags/dicas de marcadores de anúncios para que o TVSDK possa reconhecer e usar `MediaPlayerItemConfig.subscribedTags` e notificar seu aplicativo sobre tags adicionais que possam ter informações de fluxo de trabalho de publicidade.

Um possível uso de um resolvedor personalizado é para períodos de blecaute. Para lidar com esses períodos, seu aplicativo poderia implementar e registrar um detector de oportunidade de blecaute responsável pelo gerenciamento de tags de blecaute. Quando o TVSDK encontra essa tag, ele chama todos os resolvedores de conteúdo registrados para localizar o primeiro que manipula a tag especificada. Neste exemplo, é o resolvedor de conteúdo de blecaute, que pode, por exemplo, substituir o item atual por conteúdo alternativo no player pela duração especificada pela tag .