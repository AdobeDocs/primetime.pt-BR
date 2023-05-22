---
description: Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.
title: Personalizar detectores de oportunidades e resolvedores de conteúdo
exl-id: 0721278c-e128-4afc-ae81-4f23c2644859
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Visão geral {#customize-opportunity-detectors-and-content-resolvers-overiew}

Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.

O TVSDK inclui detectores de oportunidade padrão:

* `SpliceOutOpportunityDetector`, que entende as dicas de anúncios padrão
* `AdSignalingModeOpportunityGenerator`, responsável por criar oportunidades iniciais de posicionamento de anúncios com base no modo de sinalização de anúncios
* `SpliceOutOpportunityGenerator`, responsável por criar oportunidades de posicionamento de anúncios em qualquer tag #EXT-X-CUE

O TVSDK também inclui um resolvedor de conteúdo padrão que fornece conteúdo a ser inserido com base na chave de metadados no item do reprodutor:

* `AuditudeResolver`, capaz de se comunicar com os servidores do Adobe Primetime Ad Decisioning (anteriormente conhecidos como Auditude) e retornar ad breaks a serem colocados.

É possível substituir os detectores de oportunidade e resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção de tag personalizada
* Reconhecer tags personalizadas para inserção de anúncio
* Criar um provedor de anúncios personalizado
* Conteúdo de blecaute
