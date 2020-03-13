---
description: Você pode converter qualquer um dos fluxos de um aplicativo remetente baseado em TVSDK e reproduzir o fluxo no Chromecast com o Browser TVSDK.
seo-description: Você pode converter qualquer um dos fluxos de um aplicativo remetente baseado em TVSDK e reproduzir o fluxo no Chromecast com o Browser TVSDK.
seo-title: Aplicativo Google Cast para TVSDK do navegador
title: Aplicativo Google Cast para TVSDK do navegador
uuid: 018143e2-143a-4f88-97c6-4b10a2083f9e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Aplicativo Google Cast para TVSDK do navegador{#google-cast-app-for-browser-tvsdk}

Você pode converter qualquer um dos fluxos de um aplicativo remetente baseado em TVSDK e reproduzir o fluxo no Chromecast com o Browser TVSDK.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

Há dois componentes de um aplicativo ativado para Cast:

* O aplicativo remetente, que atua como controle remoto.

   Aplicativos para remetentes incluem smartphones, computadores pessoais e assim por diante. O aplicativo pode ser desenvolvido usando SDKs nativos para iOS, Android e Chrome.
* O aplicativo receptor, que é executado no Chromecast e reproduz o conteúdo.

   >[!IMPORTANT]
   >
   >Este aplicativo só pode ser um aplicativo HTML5.

O remetente e o receptor se comunicam usando os SDKs de transmissão para enviar mensagens.

## Fluxo de trabalho básico {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

Esta é uma visão geral do processo:

1. O aplicativo remetente estabelece uma conexão com o aplicativo receptor.
1. O aplicativo remetente envia uma mensagem para carregar a mídia no aplicativo receptor.
1. O aplicativo receptor inicia a reprodução.
1. O aplicativo remetente envia mensagens de controle de reprodução, como reproduzir, pausar, buscar, avançar rapidamente, retroceder, retroceder, alterar volume e assim por diante, para o aplicativo receptor.
1. O aplicativo receptor reage a essas mensagens.

## Formato de mensagem {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

É necessário definir as mensagens para que o remetente e o destinatário possam entendê-las. Este é um exemplo de uma mensagem de busca:

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

Ao enviar mensagens personalizadas, como a mensagem de busca por meio dos SDKs de transmissão, é necessário um namespace de mensagem personalizado. Este é um exemplo em JavaScript:

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## Estabelecendo uma conexão {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>As APIs TVSDK do navegador não são envolvidas ao estabelecer a conexão.

Para estabelecer uma conexão, o remetente e o destinatário devem realizar as seguintes tarefas:

* O remetente deve revisar a documentação da plataforma em Desenvolvimento [de aplicativo do](https://developers.google.com/cast/docs/sender_apps)remetente.
* O receptor usa as APIs de receptor de transmissão para estabelecer uma conexão com o aplicativo remetente. Por exemplo:

   ```js
   window.castReceiverManager = cast.receiver.CastReceiverManager.getInstance(); 
   
   window.castReceiverManager.onReady = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderConnected = function (event) { /*handle event*/ }; 
   window.castReceiverManager.onSenderDisconnected = function (event) { /*handle event*/ }; 
   
   var customMessageBus = window.castReceiverManager.getCastMessageBus(MSG_NAMESPACE); 
   customMessageBus.onMessage = function (event) { /*handle messages*/ }; 
   
   window.castReceiverManager.start(); 
   ```

## Tratamento de mensagens {#section_3E4814546F5946C9B3E7A1AE384B4FF8}

Para enviar mensagens ao receptor, consulte a documentação da plataforma do remetente.

>[!IMPORTANT]
>
>Você deve incluir o namespace personalizado da mensagem, `MSG_NAMESPACE` em todas as mensagens.

Para o aplicativo receptor, siga a documentação das APIs de receptor de difusão.

**Exemplo de uma mensagem de remetente com base no Chrome**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Tratamento de eventos de remetente com base no Chrome**

Vincule manipuladores de eventos aos elementos da interface do usuário que enviarão mensagens quando os eventos correspondentes forem acionados. Por exemplo, para um aplicativo remetente baseado no Chrome, o evento de busca pode ser enviado desta forma:

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**Tratamento de mensagens do receptor**

No aplicativo receptor, veja um exemplo de como lidar com a mensagem de busca:

```js
customMessageBus.onMessage = function (event) { 
    var message = JSON.parse(event.data); 
    switch (message.type) { 
        case "seek":  
            player.seek(parseInt(message.seekTo)); 
            break; 
        //code for handling other events 
        default:  
            break; 
    } 
}; 
```

