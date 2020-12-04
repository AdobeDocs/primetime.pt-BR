---
description: Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
seo-description: Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
seo-title: Personalizar detectores de oportunidade e resolvedores de conteúdo
title: Personalizar detectores de oportunidade e resolvedores de conteúdo
uuid: 7bd04c8f-6f04-4321-88e8-9bb93251d940
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---


# Visão geral {#customize-opportunity-detectors-and-content-resolvers-overiew}

Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas ao resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK inclui detectores de oportunidade padrão:

* `SpliceOutOpportunityDetector`, que entende dicas de anúncios padrão
* `AdSignalingModeOpportunityGenerator`, que é responsável por criar oportunidades iniciais de colocação de anúncios com base no modo de sinalização de anúncios
* `SpliceOutOpportunityGenerator`, responsável pela criação de oportunidades de colocação de anúncios a partir de qualquer tag #EXT-X-CUE

O TVSDK também inclui um resolvedor de conteúdo padrão que fornece conteúdo a ser inserido com base na chave de metadados no item do player:

* `AuditudeResolver`, capaz de se comunicar com os servidores de decisão de anúncio da Adobe Primetime (anteriormente conhecidos como Auditude) e de retornar as pausas de anúncio a serem colocadas.

Você pode substituir os detectores de oportunidade padrão e os resolvedores de conteúdo para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção de tags personalizadas
* Reconhecer tags personalizadas para inserção de anúncios
* Criar um provedor de publicidade personalizado
* Preencher conteúdo

