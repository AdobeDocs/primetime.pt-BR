---
description: Você pode converter qualquer um dos fluxos de um aplicativo de remetente baseado em TVSDK e reproduzir o fluxo no Chromecast com o TVSDK do navegador.
title: Aplicativo Google Cast para TVSDK do navegador
exl-id: 71077467-8040-4f04-a43b-cc963701c426
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Aplicativo Google Cast para TVSDK do navegador{#google-cast-app-for-browser-tvsdk}

Você pode converter qualquer um dos fluxos de um aplicativo de remetente baseado em TVSDK e reproduzir o fluxo no Chromecast com o TVSDK do navegador.

<!--<a id="section_87CE5D6D46F0439EB6E63A742D6DD9C8"></a>-->

Há dois componentes de um aplicativo habilitado para Conversão:

* O aplicativo do remetente, que atua como controle remoto.

   Os aplicativos de remetente incluem smartphones, computadores pessoais e assim por diante. O aplicativo pode ser desenvolvido usando SDKs nativos para iOS, Android e Chrome.
* O aplicativo receptor, que é executado no Chromecast e reproduz o conteúdo.

   >[!IMPORTANT]
   >
   >Este aplicativo só pode ser um aplicativo HTML5.

O remetente e o destinatário se comunicam usando os SDKs de conversão para enviar mensagens.

## Fluxo de trabalho básico {#section_FAF680FF29DA4D24A50AC0A2B6402B58}

Esta é uma visão geral do processo:

1. O aplicativo remetente estabelece uma conexão com o aplicativo receptor.
1. O aplicativo remetente envia uma mensagem para carregar a mídia no aplicativo receptor.
1. O aplicativo receptor inicia a reprodução.
1. O aplicativo do remetente envia mensagens de controle de reprodução, como reproduzir, pausar, buscar, avançar rapidamente, retroceder rapidamente, retroceder, alterar volume e assim por diante, para o aplicativo receptor.
1. O aplicativo receptor reage a essas mensagens.

## Formato da mensagem {#section_1624159DD51D4C87B3E5803DEEBCB6B7}

Você deve definir as mensagens para que o remetente e o destinatário possam entender. Veja um exemplo de uma mensagem de busca:

```js
{ 
"type": "seek", 
"seekTo": 10000 
} 
```

Ao enviar mensagens personalizadas, como a mensagem de busca por meio dos SDKs do Cast, é necessário um namespace de mensagem personalizado. Veja um exemplo em JavaScript:

```js
Custom Message Namespace 
var MSG_NAMESPACE = "urn:x-cast:com.adobe.primetime"; 
```

## Estabelecimento de uma conexão {#section_B4D40CABDD3E46FDBE7B5651DFF91653}

>[!IMPORTANT]
>
>As APIs TVSDK do navegador não estão envolvidas ao estabelecer a conexão.

Para estabelecer uma conexão, o remetente e o destinatário devem concluir as seguintes tarefas:

* O remetente deve revisar a documentação da plataforma em [Desenvolvimento de aplicativo do remetente](https://developers.google.com/cast/docs/sender_apps).
* O receptor usa as APIs do receptor Cast para estabelecer uma conexão com o aplicativo do remetente. Por exemplo:

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

Para enviar mensagens ao destinatário, consulte a documentação da plataforma do remetente.

>[!IMPORTANT]
>
>Você deve incluir o namespace de mensagem personalizado, `MSG_NAMESPACE` em todas as mensagens.

Para o aplicativo receptor, siga a documentação das APIs do receptor de transmissão.

**Exemplo de uma mensagem de remetente com base no Chrome**

```js
window.session.sendMessage(MSG_NAMESPACE, message, successCallback, errorCallback); //https://developers.google.com/cast/docs/reference/chrome/chrome.cast.Session#sendMessage
```

**Manipulação de evento do remetente com base no Chrome**

Vincule manipuladores de eventos aos elementos da interface do usuário que enviarão mensagens quando os eventos correspondentes forem acionados. Por exemplo, para um aplicativo de remetente baseado no Chrome, o evento de busca pode ser enviado da seguinte maneira:

```js
document.getElementById("#seekBar").addEventListener("click", seekEventHandler); 
   
function seekEventHandler(event) { 
    seekMessage = { type: "seek", seekTo: player.currentTime }; //player is an instance of AdobePSDK.MediaPlayer 
    window.session.sendMessage(MSG_NAMESPACE, seekMessage, successCallback, errorCallback); 
} 
```

**Tratamento de mensagens do receptor**

No aplicativo receptor, há um exemplo de como lidar com a mensagem de busca:

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
