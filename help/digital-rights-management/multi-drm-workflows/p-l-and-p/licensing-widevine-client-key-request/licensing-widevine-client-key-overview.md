---
description: Para reproduzir o conteúdo DASH resultante da embalagem do conteúdo, o cliente TVSDK precisará obter a chave de descriptografia de conteúdo transmitida durante o processo de empacotamento no fluxo de trabalho de aquisição de chave. A chave de descriptografia de conteúdo do cliente geralmente é entregue ao cliente por um servidor de licença Widevine/PlayReady em resposta a uma ou mais publicações HTTP/HTTPS do cliente.
title: Visão geral do fluxo de trabalho de Solicitação de chave do cliente
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Fluxo de trabalho Solicitação de chave do cliente {#client-key-request-workflow-overview}

Para reproduzir o conteúdo DASH resultante da embalagem do conteúdo, o cliente TVSDK precisará obter a chave de descriptografia de conteúdo transmitida durante o processo de empacotamento no fluxo de trabalho de aquisição de chave. A chave de descriptografia de conteúdo do cliente geralmente é entregue ao cliente por um servidor de licença Widevine/PlayReady em resposta a uma ou mais publicações HTTP/HTTPS do cliente.

Para adquirir a chave de descriptografia de conteúdo, o cliente PSDK deve fazer o seguinte

* Segure a caixa de transferência de conteúdo, forneça-a à plataforma e obtenha em resposta uma solicitação principal.
* Envie a solicitação de chave para o servidor de licenças Widevine/PlayReady apropriado por meio de um POST HTTP.
* Passe a resposta do servidor para a plataforma, que extrairá a chave de descriptografia de conteúdo do cliente da resposta e a usará para descriptografia de conteúdo.

Para enviar o POST HTTP para a solicitação de chave, seu código deve passar para o cliente PSDK o URL do servidor de licença juntamente com quaisquer dados extras que precisam ser anexados à publicação. A escolha do URL e dos dados a serem enviados depende do provedor de serviços Widevine/PlayReady com o qual você trabalha. Por exemplo, se você usar o ExpressPlay para fornecer o serviço, passe o URL apropriado do servidor de licenças ExpressPlay Widevine/PlayReady e anexe à chave de saída o token ExpressPlay associado à chave de criptografia do conteúdo. Você pode obter o URL do servidor de licenças ExpressPlay Widevine/PlayReady apropriado na documentação do ExpressPlay.