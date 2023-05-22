---
description: O TVSDK fornece geradores de oportunidades e resolvedores de conteúdo padrão que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base nas oportunidades identificadas no manifesto, como indicadores para um período de blecaute.
title: Geradores de oportunidades e resolvedores de conteúdo
exl-id: 6daf7ff4-10c4-4750-8592-94a2be489473
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 0%

---

# Geradores de oportunidades e resolvedores de conteúdo{#opportunity-generators-and-content-resolvers}

O TVSDK fornece geradores de oportunidades e resolvedores de conteúdo padrão que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base nas oportunidades identificadas no manifesto, como indicadores para um período de blecaute.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que geralmente indica uma oportunidade de posicionamento de anúncio. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo, como um período de blecaute. Um *`opportunity generator`* O código identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK que essas oportunidades foram marcadas. As oportunidades são identificadas em uma linha do tempo no `TimedMetadata`. A variável `SpliceOutOpportunityGenerator` cria oportunidades com base na `TimedMetadata` objetos criados para cada tag de publicidade detectada no manifesto e a variável `AdSignalingModeOpportunityGenerator` cria a oportunidade inicial com base na `MediaPlayerItem` tipo e seu modo de sinalização de anúncio associado.

Quando seu aplicativo é notificado sobre uma oportunidade (tag), ele pode alterar a linha do tempo, por exemplo, inserindo uma série de anúncios, alternando para um fluxo alternativo (blecautes) ou editando o conteúdo da linha do tempo. Por padrão, o TVSDK chama o método apropriado *`content resolver`* para implementar as alterações ou ações de linha do tempo necessárias. Seu aplicativo pode usar o resolvedor de conteúdo de anúncios TVSDK padrão ou registrar seu próprio resolvedor de conteúdo.

Também é possível usar `PSDKConfig.adTags` para adicionar mais tags/dicas de marcador de anúncio para o padrão `SpliceOutOpportunityGenerator` classe e uso `PSDKConfig.setSubscribedTags` para que o TVSDK possa notificar seu aplicativo sobre tags adicionais que podem ter informações de fluxo de trabalho de publicidade.

Um uso possível de um resolvedor personalizado é para períodos de blecaute. Para lidar com esses períodos, sua aplicação pode implementar e registrar um detector de oportunidade de blecaute responsável por lidar com tags de blecaute. Quando o TVSDK encontra essa tag, ele pesquisa todos os resolvedores de conteúdo registrados para encontrar o primeiro que manipula a tag especificada. Neste exemplo, é o resolvedor de conteúdo de blecaute, que pode, por exemplo, substituir o item atual pelo conteúdo alternativo no reprodutor pela duração especificada pela tag.
