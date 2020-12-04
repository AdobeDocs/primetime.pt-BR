---
description: Um detector de oportunidade é um componente TVSDK do navegador que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
seo-description: Um detector de oportunidade é um componente TVSDK do navegador que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
seo-title: Personalizar detectores de oportunidade e resolvedores de conteúdo
title: Personalizar detectores de oportunidade e resolvedores de conteúdo
uuid: d4926933-5966-4cd8-8050-c81c5e3c8545
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 0%

---


# Visão geral {#customize-opportunity-detectors-and-content-resolvers-overview}

Um detector de oportunidade é um componente TVSDK do navegador que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK do navegador inclui os seguintes detectores de oportunidade padrão:

* `AdSignalingModeOpportunityGenerator`, que cria oportunidades iniciais de colocação de anúncios com base no modo de sinalização de anúncios.
* `ManifestCuesOpportunityGenerator`, que cria oportunidades de colocação de anúncios a partir de qualquer tag splice-out.

O TVSDK do navegador também inclui resolvedores de conteúdo padrão, como `AuditudeResolver`, que fornece conteúdo que será inserido com base na chave de metadados no item do player. `AuditudeResolver` é capaz de se comunicar com os servidores de decisão de anúncios da Adobe Primetime e de fazer pausas para anúncios a serem feitos.

Você pode substituir os detectores de oportunidade padrão e os resolvedores de conteúdo para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção de tags personalizadas
* Reconhecer tags personalizadas para inserção de anúncios
* Criar um provedor de publicidade personalizado

