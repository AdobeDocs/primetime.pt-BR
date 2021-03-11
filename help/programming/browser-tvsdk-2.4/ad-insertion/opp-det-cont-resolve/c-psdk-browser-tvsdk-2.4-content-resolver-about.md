---
description: O TVSDK do navegador fornece geradores de oportunidades padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto.
title: Geradores de oportunidades e resolvedores de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---


# Geradores de oportunidades e resolvedores de conteúdo{#opportunity-generators-and-content-resolvers}

O TVSDK do navegador fornece geradores de oportunidades padrão e resolvedores de conteúdo que colocam anúncios na linha do tempo, e esses geradores e resolvedores são baseados em tags não padrão no manifesto. Seu aplicativo pode precisar alterar a linha do tempo com base em oportunidades identificadas no manifesto.

Um *`opportunity`* representa um ponto de interesse na linha do tempo que geralmente indica uma oportunidade de posicionamento de anúncios. Essa oportunidade também pode indicar uma operação personalizada que pode afetar a linha do tempo. Um *`opportunity generator`* identifica oportunidades específicas (tags) na linha do tempo e notifica o TVSDK de que essas oportunidades foram marcadas.

As oportunidades são identificadas em uma linha do tempo em `TimedMetata`. O `ManifestCuesOpportunityGenerator` cria oportunidades com base nos objetos `TimedMetadata` criados para cada tag de anúncio dividida (em `MediaPlayerItemConfig.adTags`) que foi detectada no manifesto. O `AdSignalingModeOpportunityGenerator` cria a oportunidade inicial baseada no tipo `MediaPlayerItem` e no modo associado de sinalização de anúncios.

>[!TIP]
>
>Se a propriedade `AdvertisingMetadata.livePreroll` ou `AdvertisingMetadata.preroll` estiver definida, `AdSignalingModeOpportunityGenerator` gera uma oportunidade antes da exibição para fluxos ao vivo.

Quando seu aplicativo é notificado sobre uma oportunidade (tag), seu aplicativo pode alterar a linha do tempo inserindo, por exemplo, uma série de anúncios. Por padrão, o TVSDK do navegador chama o *`content resolver`* apropriado para implementar as alterações ou ações necessárias da linha do tempo. Seu aplicativo pode usar o resolvedor de conteúdo de anúncio padrão TVSDK do navegador ou registrar seu próprio resolvedor de conteúdo.

Você também pode usar `MediaPlayerItemConfig.adTags` para adicionar mais tags/dicas de marcador de anúncio para a classe padrão `ManifestCuesOpportunityGenerator` e usar `MediaPlayerItemConfig.subscribedTags` para que o TVSDK possa notificar seu aplicativo sobre tags adicionais que podem ter informações de fluxo de trabalho de publicidade.

>[!TIP]
>
>Os valores padrão de `MediaPlayerItemConfig.adTags` e `MediaPlayerItemConfig.subscribeTags` são `[MediaPlayerItemConfig.DEFAULT_AD_TAG]`.

