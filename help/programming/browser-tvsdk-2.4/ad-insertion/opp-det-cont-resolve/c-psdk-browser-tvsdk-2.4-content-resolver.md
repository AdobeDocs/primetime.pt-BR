---
description: Um detector de oportunidade é um componente TVSDK do navegador que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
title: Personalizar detectores de oportunidade e resolvedores de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Visão geral {#customize-opportunity-detectors-and-content-resolvers-overview}

Um detector de oportunidade é um componente TVSDK do navegador que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK do navegador inclui os seguintes detectores de oportunidade padrão:

* `AdSignalingModeOpportunityGenerator`, que cria oportunidades de posicionamento do anúncio inicial com base no modo de sinalização do anúncio.
* `ManifestCuesOpportunityGenerator`, que cria oportunidades de posicionamento de anúncios a partir de qualquer tag de separação.

O TVSDK do navegador também inclui resolvedores de conteúdo padrão, como `AuditudeResolver`, que fornece conteúdo que será inserido com base na chave de metadados no item do player. `AuditudeResolver` O é capaz de se comunicar com os servidores de decisão de anúncios da Adobe Primetime e retornar ad breaks a serem colocados.

Você pode substituir os detectores de oportunidade e os resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção personalizada de tags
* Reconhecer tags personalizadas para inserção de anúncios
* Criar um provedor de publicidade personalizado

