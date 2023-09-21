---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido.
title: Carregar um recurso de mídia no MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# Carregar um recurso de mídia no MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido.

1. Defina seu `MediaPlayer` item reproduzível do objeto com o novo recurso a ser reproduzido.

   Substituir seu existente `MediaPlayer` item reproduzível no momento chamando `replaceCurrentResource` e transmitindo um existente `MediaResource` instância.

1. Aguardar o TVSDK do navegador despachar `AdobePSDK.MediaPlayerStatusChangeEvent` com `event.status` que seja igual a qualquer uma das seguintes opções:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

     Por meio desses eventos, o objeto MediaPlayer notifica seu aplicativo se o recurso de mídia foi carregado com êxito.

1. Quando o estado do reprodutor de mídia muda para `MediaPlayerStatus.INITIALIZED`, você pode chamar `MediaPlayer.prepareToPlay`.

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamando `prepareToPlay` inicia o processo de resolução e posicionamento do anúncio, se houver.
1. Quando o TVSDK do navegador despacha a variável `MediaPlayerStatus.PREPARED` caso o fluxo de mídia tenha sido carregado com êxito (um MediaPlayerItem foi criado) e esteja preparado para reprodução.

Se ocorrer uma falha, a variável `MediaPlayer` alterna para o `MediaPlayerStatus.ERROR`.

Ele também notifica seu aplicativo enviando o `MediaPlayerStatus.ERROR` evento.

><!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

O código de amostra simplificado a seguir ilustra o processo de carregamento de um recurso de mídia:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                        onStatusChange); 
 
onStatusChange = function (event) { 
    var msg = ""; 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            msg = "Player Status: INITIALIZED"; 
            console.log(msg); 
            player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
        // The resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback. 
        // Once the resource is loaded, the MediaPlayer can 
        // provide a reference to the current "playable item" 
           MediaPlayerItem playerItem = player.currentItem; 
           if (playerItem != null) {  
              // here we can look at the properties of the  
              // loadedstream 
           } 
           break; 
    } 
}
```
