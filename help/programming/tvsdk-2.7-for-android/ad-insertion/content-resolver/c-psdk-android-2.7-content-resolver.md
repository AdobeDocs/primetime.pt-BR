---
description: Um gerador de oportunidades identifica oportunidades de posicionamento por tags personalizadas em um fluxo, marcadores personalizados do modo de sinalização e assim por diante. O gerador de oportunidades envia essas oportunidades de posicionamento para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.
title: Personalizar geradores de oportunidades e resolvedores de conteúdo
exl-id: 2ce859c4-6bf6-4ec5-82b1-2bc6a2316fd9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Visão geral {#customize-opportunity-generators-and-content-resolvers-overview}

Um gerador de oportunidades identifica oportunidades de posicionamento por tags personalizadas em um fluxo, marcadores personalizados do modo de sinalização e assim por diante. O gerador de oportunidades envia essas oportunidades de posicionamento para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.

O TVSDK inclui os seguintes geradores de oportunidade padrão:

* `ManifestCuesOpportunityGenerator` gera oportunidades a partir das dicas de publicidade padrão ( `#EXT-X-CUE`).

* `AdSignalingModeOpportunityGenerator` gera uma oportunidade inicial para o modo de sinalização de anúncio especificado. Isso ignora qualquer dica ou informação de metadados cronometrados.
* `CustomMarkerOpportunityGenerator` O gera oportunidades para substituir anúncios C3 elaborados.
* `AuditudeResolver`O gerador de oportunidades do produz oportunidades quando a resolução de anúncios lento está ativada.

O TVSDK também inclui resolvedores de conteúdo padrão:

* `CustomRangeResolver`
* `JSONResolver`
* `AuditudeResolver`, que pode se comunicar com o Primetime e o Decisioning.

É possível substituir os geradores de oportunidade e resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Reconhecer tags personalizadas para inserção de anúncio
* Crie um provedor de anúncios personalizado.
* Conteúdo em preto-e-branco.
