---
description: O TVSDK do navegador fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base nas oportunidades identificadas no manifesto.
seo-description: O TVSDK do navegador fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base nas oportunidades identificadas no manifesto.
seo-title: Geradores de oportunidade e resolvedores de conteúdo
title: Geradores de oportunidade e resolvedores de conteúdo
uuid: e462ad89-1609-4efa-aa67-cfd04f045927
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Geradores de oportunidade e resolvedores de conteúdo{#opportunity-generators-and-content-resolvers}

O TVSDK do navegador fornece geradores de oportunidade padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base nas oportunidades identificadas no manifesto.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que normalmente indica uma oportunidade de colocação de anúncio. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo. Um *`opportunity generator`* identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK de que essas oportunidades foram marcadas.

As oportunidades são identificadas em uma linha do tempo em `TimedMetata`. O `ManifestCuesOpportunityGenerator` cria oportunidades com base nos objetos `TimedMetadata` criados para cada tag de anúncio dividida (em `MediaPlayerItemConfig.adTags`) que foi detectada no manifesto. O `AdSignalingModeOpportunityGenerator` cria a oportunidade inicial baseada no tipo `MediaPlayerItem` e no modo associado de sinalização de anúncios.

>[!TIP]
>
>Se a propriedade `AdvertisingMetadata.livePreroll` ou `AdvertisingMetadata.preroll` estiver definida, `AdSignalingModeOpportunityGenerator` gerará uma oportunidade de precedente para fluxos ao vivo.

Quando seu aplicativo é notificado sobre uma oportunidade (tag), seu aplicativo pode alterar a linha do tempo inserindo, por exemplo, uma série de anúncios. Por padrão, o TVSDK do navegador chama o *`content resolver`* apropriado para implementar as alterações ou ações necessárias na linha do tempo. Seu aplicativo pode usar o resolvedor de conteúdo de anúncio TVSDK do navegador padrão ou registrar seu próprio resolvedor de conteúdo.

Você também pode usar `MediaPlayerItemConfig.adTags` para adicionar mais tags/dicas de marcador de anúncio para a classe `ManifestCuesOpportunityGenerator` padrão e usar `MediaPlayerItemConfig.subscribedTags` para que o TVSDK possa notificar seu aplicativo sobre tags adicionais que possam ter informações de fluxo de trabalho de publicidade.

>[!TIP]
>
>Os valores padrão de `MediaPlayerItemConfig.adTags` e `MediaPlayerItemConfig.subscribeTags` são `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

