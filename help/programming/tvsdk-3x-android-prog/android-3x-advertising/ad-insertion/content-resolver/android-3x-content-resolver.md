---
description: Um gerador de oportunidades identifica oportunidades de colocação por tags personalizadas em um fluxo, marcadores personalizados no modo de sinalização de anúncios e assim por diante. O gerador de oportunidades envia essas oportunidades de posicionamento ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
seo-description: Um gerador de oportunidades identifica oportunidades de colocação por tags personalizadas em um fluxo, marcadores personalizados no modo de sinalização de anúncios e assim por diante. O gerador de oportunidades envia essas oportunidades de posicionamento ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
seo-title: Personalizar geradores de oportunidade e resolvedores de conteúdo
title: Personalizar geradores de oportunidade e resolvedores de conteúdo
uuid: 0d4fb0b2-98f3-4245-9bf1-4e968c5d0f36
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---


# Visão geral {#customize-opportunity-generators-and-content-resolvers-overview}

Um gerador de oportunidades identifica oportunidades de colocação por tags personalizadas em um fluxo, marcadores personalizados no modo de sinalização de anúncios e assim por diante. O gerador de oportunidades envia essas oportunidades de posicionamento ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK inclui os seguintes geradores de oportunidade padrão:

* `ManifestCuesOpportunityGenerator` gera oportunidades a partir das dicas de anúncio padrão (  `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` gera uma oportunidade inicial para o modo de sinalização de anúncio especificado. Isso ignora quaisquer dicas ou informações de metadados cronometrados.
* `CustomMarkerOpportunityGenerator` gera oportunidades para substituir anúncios integrados em C3.
* `AuditudeResolver`O gerador de oportunidades do produz oportunidades quando a resolução de anúncios ociosos está ativada.

O TVSDK também inclui os resolvedores de conteúdo padrão:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que pode se comunicar com a decisão do anúncio Primetime.

Você pode substituir os geradores de oportunidade padrão e os resolvedores de conteúdo para personalizar o fluxo de trabalho de publicidade de maneiras como as seguintes:

* Reconhecer tags personalizadas para inserção de anúncios. Para obter mais informações, consulte [Personalizar geradores de oportunidade e resolvedores de conteúdo](../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/content-resolver/android-3x-content-resolver.md).
* Crie um provedor de publicidade personalizado.
* Preencha o conteúdo.