---
description: Um gerador de oportunidades identifica oportunidades de posicionamento por tags personalizadas em um fluxo, marcadores personalizados do modo de sinalização de anúncios e assim por diante. O gerador de oportunidades envia essas oportunidades de posicionamento para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
title: Personalizar geradores de oportunidades e resolvedores de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---


# Visão geral {#customize-opportunity-generators-and-content-resolvers-overview}

Um gerador de oportunidades identifica oportunidades de posicionamento por tags personalizadas em um fluxo, marcadores personalizados do modo de sinalização de anúncios e assim por diante. O gerador de oportunidades envia essas oportunidades de posicionamento para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK inclui os seguintes geradores de oportunidade padrão:

* `ManifestCuesOpportunityGenerator` gera oportunidades com base nas dicas de anúncio padrão (  `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` gera uma oportunidade inicial para o modo de sinalização de anúncio especificado. Isso ignora quaisquer dicas ou informações de metadados cronometrados.
* `CustomMarkerOpportunityGenerator` gera oportunidades para substituir anúncios em C3 integrados.
* `AuditudeResolver`O gerador de oportunidades do produz oportunidades quando a resolução de anúncios ociosos está ativada.

O TVSDK também inclui resolvedores de conteúdo padrão:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que pode se comunicar com o Primetime ad decisioning.

Você pode substituir os geradores de oportunidade e os resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade de formas como as seguintes:

* Reconhecer tags personalizadas para inserção de anúncios
* Crie um provedor de publicidade personalizado.
* Conteúdo preto.