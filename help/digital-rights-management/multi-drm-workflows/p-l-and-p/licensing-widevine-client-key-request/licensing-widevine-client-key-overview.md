---
description: Para reproduzir o conteúdo DASH resultante do empacotamento de conteúdo, o cliente TVSDK precisará obter a chave de descriptografia do conteúdo transmitida durante o processo de empacotamento no fluxo de trabalho de aquisição de chaves. A chave de descriptografia de conteúdo do cliente geralmente é entregue ao cliente por um servidor de licenças Widevine/PlayReady em resposta a uma ou mais publicações HTTP/HTTPS do cliente.
title: Visão geral do fluxo de trabalho de Solicitação de chave do cliente
exl-id: ae600cbd-415b-441a-bf01-f259993071f2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---

# Fluxo de trabalho de Solicitação de chave do cliente {#client-key-request-workflow-overview}

Para reproduzir o conteúdo DASH resultante do empacotamento de conteúdo, o cliente TVSDK precisará obter a chave de descriptografia do conteúdo transmitida durante o processo de empacotamento no fluxo de trabalho de aquisição de chaves. A chave de descriptografia de conteúdo do cliente geralmente é entregue ao cliente por um servidor de licenças Widevine/PlayReady em resposta a uma ou mais publicações HTTP/HTTPS do cliente.

Para adquirir a chave de descriptografia de conteúdo, o cliente PSDK deve fazer o seguinte

* Segure a caixa de push do conteúdo, dê-a à plataforma e obtenha uma solicitação principal em resposta.
* Envie a solicitação de chave para o servidor de licença Widevine/PlayReady apropriado por meio de um POST HTTP.
* Envie a resposta do servidor para a plataforma que extrairá a chave de descriptografia de conteúdo do cliente da resposta e a usará para descriptografia de conteúdo.

Para enviar o POST HTTP para a solicitação de chave, o código deve passar para o cliente PSDK o URL do servidor de licenças, juntamente com quaisquer dados adicionais que precisam ser anexados ao post. A escolha de URL e dados a serem transmitidos depende do provedor de serviços Widevine/PlayReady com o qual você trabalha. Por exemplo, se você usar o ExpressPlay para fornecer o serviço, transmita o URL do servidor de licença ExpressPlay Widevine/PlayReady apropriado e anexe à solicitação de chave de saída o token ExpressPlay associado à chave de criptografia do conteúdo. Você pode obter o URL do servidor de licença ExpressPlay Widevine/PlayReady apropriado na documentação do ExpressPlay.
