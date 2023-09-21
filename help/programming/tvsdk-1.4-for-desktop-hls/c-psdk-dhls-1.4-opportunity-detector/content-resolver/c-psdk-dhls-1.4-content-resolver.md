---
description: Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.
title: Personalizar detectores de oportunidades e resolvedores de conteúdo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Visão geral {#customize-opportunity-detectors-and-content-resolvers-overiew}

Um detector de oportunidade é um componente TVADK que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.

O TVSDK inclui detectores de oportunidade padrão:

* `SpliceOutOpportunityDetector`, que entende as dicas de publicidade padrão
* `AdSignalingModeOpportunityGenerator`, responsável por criar oportunidades iniciais de posicionamento de anúncios com base no modo de sinalização de anúncios
* `SpliceOutOpportunityGenerator`, responsável por criar oportunidades de posicionamento de anúncios em qualquer tag #EXT-X-CUE

O TVSDK também inclui um resolvedor de conteúdo padrão que fornece conteúdo a ser inserido com base na chave de metadados no item do reprodutor:

* `AuditudeResolver`, capaz de se comunicar com os servidores do Adobe Primetime ad decisioning (anteriormente conhecidos como Auditude) e de retornar ad breaks a serem colocados.

É possível substituir os detectores de oportunidade e resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção de tag personalizada
* Reconhecer tags personalizadas para inserção de anúncio
* Criar um provedor de anúncios personalizado
* Conteúdo de blecaute
