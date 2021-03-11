---
description: O TVSDK entra em contato com um serviço de entrega de anúncios, como o Adobe Primetime Ad Decisioning, e tenta obter o arquivo de lista de reprodução principal que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK faz uma chamada HTTP para o servidor remoto de entrega de anúncios e analisa a resposta do servidor.
title: Fase de resolução de anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '291'
ht-degree: 0%

---


# Fase de resolução de anúncios{#ad-resolving-phase}

O TVSDK entra em contato com um serviço de entrega de anúncios, como o Adobe Primetime Ad Decisioning, e tenta obter o arquivo de lista de reprodução principal que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK faz uma chamada HTTP para o servidor remoto de entrega de anúncios e analisa a resposta do servidor.

O TVSDK é compatível com os seguintes tipos de provedores de anúncios:

* Provedor de publicidade de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão do Primetime

   O TVSDK envia uma solicitação, incluindo um conjunto de parâmetros de direcionamento e um número de identificação do ativo, para o servidor de back-end do Primetime ad decisioning. O Primetime ad decisioning responde com um documento SMIL (linguagem de integração de multimídia sincronizada) que contém as informações de anúncio necessárias.
* Provedor de marcadores de anúncio personalizados

   Gerencia a situação em que os anúncios são gravados no stream, a partir do lado do servidor. O TVSDK não executa a inserção de anúncio real, mas precisa rastrear os anúncios que foram inseridos no lado do servidor. Esse provedor define os marcadores de anúncios que o TVSDK usa para executar o rastreamento de anúncios.

Uma das seguintes situações de failover pode ocorrer durante esta fase:

* Os dados não podem ser recuperados por motivos que incluem falta de conectividade ou um erro no lado do servidor, como um recurso não pode ser encontrado e assim por diante.
* Os dados foram recuperados, mas o formato é inválido.

   Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.
