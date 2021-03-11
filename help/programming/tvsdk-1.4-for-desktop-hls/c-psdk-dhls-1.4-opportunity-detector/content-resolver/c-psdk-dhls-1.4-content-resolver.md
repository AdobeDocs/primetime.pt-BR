---
description: Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.
title: Personalizar detectores de oportunidade e resolvedores de conteúdo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---


# Visão geral {#customize-opportunity-detectors-and-content-resolvers-overiew}

Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e metadados da oportunidade de posicionamento.

O TVSDK inclui detectores de oportunidade padrão:

* `SpliceOutOpportunityDetector`, que entende as dicas de anúncio padrão
* `AdSignalingModeOpportunityGenerator`, que é responsável por criar oportunidades de posicionamento do anúncio inicial com base no modo de sinalização do anúncio
* `SpliceOutOpportunityGenerator`, que é responsável por criar oportunidades de colocação de anúncios em qualquer tag #EXT-X-CUE

O TVSDK também inclui um resolvedor de conteúdo padrão que fornece conteúdo a ser inserido com base na chave de metadados no item do reprodutor:

* `AuditudeResolver`, capaz de se comunicar com os servidores Adobe Primetime ad decisioning (anteriormente conhecidos como Auditude) e retornar ad breaks para serem colocados.

Você pode substituir os detectores de oportunidade e os resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção personalizada de tags
* Reconhecer tags personalizadas para inserção de anúncios
* Criar um provedor de publicidade personalizado
* Conteúdo preto

