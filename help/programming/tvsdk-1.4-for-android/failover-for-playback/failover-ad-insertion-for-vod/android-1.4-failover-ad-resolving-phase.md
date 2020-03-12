---
description: O TVSDK entra em contato com um serviço de entrega de anúncios, como a decisão do anúncio do Adobe Primetime, e tenta obter o arquivo principal da lista de reprodução que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK efetua uma chamada HTTP para o servidor de entrega de anúncios remoto e analisa a resposta do servidor.
seo-description: O TVSDK entra em contato com um serviço de entrega de anúncios, como a decisão do anúncio do Adobe Primetime, e tenta obter o arquivo principal da lista de reprodução que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK efetua uma chamada HTTP para o servidor de entrega de anúncios remoto e analisa a resposta do servidor.
seo-title: Fase de resolução de anúncios
title: Fase de resolução de anúncios
uuid: b3e62a57-7e62-4e4e-8fa6-0d416785db67
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Fase de resolução de anúncios{#ad-resolving-phase}

O TVSDK entra em contato com um serviço de entrega de anúncios, como a decisão do anúncio do Adobe Primetime, e tenta obter o arquivo principal da lista de reprodução que corresponde ao fluxo de vídeo do anúncio. Durante a fase de resolução de anúncios, o TVSDK efetua uma chamada HTTP para o servidor de entrega de anúncios remoto e analisa a resposta do servidor.

O TVSDK oferece suporte aos seguintes tipos de provedores de anúncios:

* Provedor de publicidade de metadados

   Os dados do anúncio são codificados em arquivos JSON de texto simples.
* Provedor de anúncios de decisão do Primetime

   O TVSDK envia uma solicitação, incluindo um conjunto de parâmetros de definição de metas e um número de identificação do ativo, para o servidor back-end de decisão do anúncio Primetime. A decisão do anúncio Primetime responde com um documento SMIL (sincronized multimedia integration language) que contém as informações necessárias do anúncio.
* Provedor personalizado de marcadores de anúncio

   Gerencia a situação em que os anúncios são gravados no stream, a partir do servidor. O TVSDK não executa a inserção real do anúncio, mas precisa rastrear os anúncios que foram inseridos no servidor. Esse provedor define os marcadores de anúncio que o TVSDK usa para executar o rastreamento de anúncio.

Uma das seguintes situações de failover pode ocorrer durante essa fase:

* Os dados não podem ser recuperados por motivos que incluem falta de conectividade ou erro no lado do servidor, como um recurso não encontrado e assim por diante.
* Os dados foram recuperados, mas o formato é inválido.

   Isso pode ocorrer porque, por exemplo, a análise dos dados de entrada falhou.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.
