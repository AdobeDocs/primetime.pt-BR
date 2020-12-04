---
description: Para reproduzir o conteúdo DASH resultante da embalagem do conteúdo, o cliente TVSDK precisará obter a chave de decodificação do conteúdo transmitida durante o processo de empacotamento no fluxo de trabalho de aquisição da chave. A chave de decodificação de conteúdo do cliente é normalmente entregue ao cliente por um servidor de licença Widevine/PlayReady em resposta a uma ou mais publicações HTTP/HTTPS do cliente.
seo-description: Para reproduzir o conteúdo DASH resultante da embalagem do conteúdo, o cliente TVSDK precisará obter a chave de decodificação do conteúdo transmitida durante o processo de empacotamento no fluxo de trabalho de aquisição da chave. A chave de decodificação de conteúdo do cliente é normalmente entregue ao cliente por um servidor de licença Widevine/PlayReady em resposta a uma ou mais publicações HTTP/HTTPS do cliente.
seo-title: Visão geral do fluxo de trabalho da Solicitação de chave do cliente
title: Visão geral do fluxo de trabalho da Solicitação de chave do cliente
uuid: 2f01f0ae-adbf-42fa-a908-4b5b9410a26d
translation-type: tm+mt
source-git-commit: ffb993889a78ee068b9028cb2bd896003c5d4d4c
workflow-type: tm+mt
source-wordcount: '371'
ht-degree: 0%

---


# Fluxo de trabalho de solicitação de chave do cliente {#client-key-request-workflow-overview}

Para reproduzir o conteúdo DASH resultante da embalagem do conteúdo, o cliente TVSDK precisará obter a chave de decodificação do conteúdo transmitida durante o processo de empacotamento no fluxo de trabalho de aquisição da chave. A chave de decodificação de conteúdo do cliente é normalmente entregue ao cliente por um servidor de licença Widevine/PlayReady em resposta a uma ou mais publicações HTTP/HTTPS do cliente.

Para adquirir a chave de decodificação de conteúdo, o cliente PSDK deve fazer o seguinte:

* Segure a caixa pssh do conteúdo, forneça-a à plataforma e obtenha em resposta uma solicitação chave.
* Envie a solicitação de chave para o servidor de licença apropriado do Widevine/PlayReady por meio de um POST HTTP.
* Passe a resposta do servidor para a plataforma que extrairá a chave de decodificação de conteúdo do cliente da resposta e a usará para decodificação de conteúdo.

Para enviar o POST HTTP para a solicitação de chave, seu código deve passar para o cliente PSDK o URL do servidor de licença juntamente com quaisquer dados adicionais que precisem ser anexados à publicação. A escolha do URL e dos dados a serem enviados depende do provedor de serviço Widevine/PlayReady com o qual você trabalha. Por exemplo, se você usa o ExpressPlay para fornecer o serviço, passa o URL do servidor de licença ExpressPlay Widevine/PlayReady apropriado e anexa à chave de saída que solicita o token ExpressPlay associado à chave de criptografia do conteúdo. Você pode obter o URL do servidor de licenças ExpressPlay Widevine/PlayReady apropriado na documentação do ExpressPlay.