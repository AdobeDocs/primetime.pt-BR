---
description: Um detector de oportunidades é um componente TVSDK do navegador que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.
title: Personalizar detectores de oportunidades e resolvedores de conteúdo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Visão geral {#customize-opportunity-detectors-and-content-resolvers-overview}

Um detector de oportunidades é um componente TVSDK do navegador que detecta tags personalizadas em um fluxo e identifica oportunidades de posicionamento. Essas oportunidades são enviadas para o resolvedor de conteúdo, que personaliza o fluxo de trabalho de inserção de conteúdo/anúncio com base nas propriedades e nos metadados da oportunidade de posicionamento.

O TVSDK do navegador inclui os seguintes detectores de oportunidade padrão:

* `AdSignalingModeOpportunityGenerator`, que cria oportunidades iniciais de posicionamento de anúncios com base no modo de sinalização de anúncios.
* `ManifestCuesOpportunityGenerator`, que cria oportunidades de posicionamento de anúncios a partir de qualquer tag de divisão.

O TVSDK do navegador também inclui resolvedores de conteúdo padrão, como `AuditudeResolver`, que fornece o conteúdo que será inserido com base na chave de metadados no item do reprodutor. `AuditudeResolver` O é capaz de se comunicar com os servidores do Adobe Primetime ad decisioning e retornar ad breaks a serem colocados.

É possível substituir os detectores de oportunidade e resolvedores de conteúdo padrão para personalizar o fluxo de trabalho de publicidade das seguintes maneiras:

* Adicionar suporte para detecção de tag personalizada
* Reconhecer tags personalizadas para inserção de anúncio
* Criar um provedor de anúncios personalizado
