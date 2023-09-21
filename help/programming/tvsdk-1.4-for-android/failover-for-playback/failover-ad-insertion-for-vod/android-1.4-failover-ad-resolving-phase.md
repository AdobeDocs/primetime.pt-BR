---
description: O TVSDK entra em contato com um serviço de entrega de anúncios, como o Adobe Primetime Ad Decisioning, e tenta obter o arquivo de lista de reprodução principal que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK faz uma chamada HTTP para o servidor remoto de entrega de anúncios e analisa a resposta do servidor.
title: Fase de resolução de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---

# Fase de resolução de anúncios{#ad-resolving-phase}

O TVSDK entra em contato com um serviço de entrega de anúncios, como o Adobe Primetime Ad Decisioning, e tenta obter o arquivo de lista de reprodução principal que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK faz uma chamada HTTP para o servidor remoto de entrega de anúncios e analisa a resposta do servidor.

O TVSDK é compatível com os seguintes tipos de provedores de anúncios:

* Provedor de anúncio de metadados

  Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão de anúncio do Primetime

  O TVSDK envia uma solicitação, incluindo um conjunto de parâmetros de direcionamento e um número de identificação de ativo, para o servidor back-end do Primetime ad Decisioning. O Primetime ad Decisioning responde com um documento SMIL (linguagem de integração multimídia sincronizada) que contém as informações de anúncio necessárias.
* Provedor de marcadores de anúncios personalizados

  Trata a situação em que os anúncios são gravados no fluxo, a partir do lado do servidor. O TVSDK não executa a inserção real do anúncio, mas precisa acompanhar os anúncios inseridos no lado do servidor. Esse provedor define os marcadores de anúncios que o TVSDK usa para executar o rastreamento de anúncios.

Uma das seguintes situações de failover pode ocorrer durante essa fase:

* Os dados não podem ser recuperados por motivos que incluem falta de conectividade ou um erro do lado do servidor, como a impossibilidade de encontrar um recurso e assim por diante.
* Os dados foram recuperados, mas o formato é inválido.

  Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.
