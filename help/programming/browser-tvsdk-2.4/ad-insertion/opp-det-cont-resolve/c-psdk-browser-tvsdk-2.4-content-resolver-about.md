---
description: O TVSDK do navegador fornece geradores de oportunidades e resolvedores de conteúdo padrão que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base nas oportunidades identificadas no manifesto.
title: Geradores de oportunidades e resolvedores de conteúdo
exl-id: a47acd22-8b1b-4c66-a7eb-a4d99afb5f17
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Geradores de oportunidades e resolvedores de conteúdo{#opportunity-generators-and-content-resolvers}

O TVSDK do navegador fornece geradores de oportunidades e resolvedores de conteúdo padrão que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base nas oportunidades identificadas no manifesto.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que geralmente indica uma oportunidade de posicionamento de anúncio. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo. Um *`opportunity generator`* O código identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK que essas oportunidades foram marcadas.

As oportunidades são identificadas em uma linha do tempo no `TimedMetata`. A variável `ManifestCuesOpportunityGenerator` cria oportunidades com base na `TimedMetadata` objetos criados para cada tag de anúncio dividida (em `MediaPlayerItemConfig.adTags`) que foi detectado no manifesto. A variável `AdSignalingModeOpportunityGenerator` cria a oportunidade inicial com base na `MediaPlayerItem` tipo e seu modo de sinalização de anúncio associado.

>[!TIP]
>
>Se a variável `AdvertisingMetadata.livePreroll` ou o `AdvertisingMetadata.preroll` é definida, `AdSignalingModeOpportunityGenerator` gera uma oportunidade de antes da exibição para fluxos ao vivo.

Quando seu aplicativo é notificado sobre uma oportunidade (tag), ele pode alterar a linha do tempo, por exemplo, inserindo uma série de anúncios. Por padrão, o TVSDK do navegador chama o *`content resolver`* para implementar as alterações ou ações de linha do tempo necessárias. Seu aplicativo pode usar o resolvedor de conteúdo de anúncios TVSDK do navegador padrão ou registrar seu próprio resolvedor de conteúdo.

Também é possível usar `MediaPlayerItemConfig.adTags` para adicionar mais tags/dicas de marcador de anúncio para o padrão `ManifestCuesOpportunityGenerator` classe e uso `MediaPlayerItemConfig.subscribedTags` para que o TVSDK possa notificar seu aplicativo sobre tags adicionais que podem ter informações de fluxo de trabalho de publicidade.

>[!TIP]
>
>Os valores padrão de `MediaPlayerItemConfig.adTags` e `MediaPlayerItemConfig.subscribeTags` é `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.
