---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido.
title: Carregar um recurso de mídia no MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Carregar um recurso de mídia no MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido.

1. Defina o item reproduzível do objeto `MediaPlayer` com o novo recurso a ser reproduzido.

   Substitua o item do objeto `MediaPlayer` existente que pode ser reproduzido, chamando `replaceCurrentResource` e transmitindo uma instância `MediaResource` existente.

1. Aguarde o TVSDK do navegador despachar `AdobePSDK.MediaPlayerStatusChangeEvent` com `event.status` que seja igual a qualquer um dos seguintes:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      Por meio desses eventos, o objeto MediaPlayer notifica o aplicativo se o recurso de mídia foi carregado com êxito.

1. Quando o estado do reprodutor de mídia for alterado para `MediaPlayerStatus.INITIALIZED`, você poderá chamar `MediaPlayer.prepareToPlay`.

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamar `prepareToPlay` inicia a resolução e o processo de posicionamento do anúncio, se houver.
1. Quando o TVSDK do navegador despacha o evento `MediaPlayerStatus.PREPARED`, o fluxo de mídia é carregado com êxito (um MediaPlayerItem é criado) e está preparado para reprodução.

Se ocorrer uma falha, o `MediaPlayer` alterna para `MediaPlayerStatus.ERROR`.

Ele também notifica seu aplicativo ao despachar o evento `MediaPlayerStatus.ERROR`.

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
