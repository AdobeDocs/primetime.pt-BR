---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido.
seo-description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido.
seo-title: Carregar um recurso de mídia no MediaPlayer
title: Carregar um recurso de mídia no MediaPlayer
uuid: ac31ccfe-161d-41a2-9a6e-38fae11ceab5
translation-type: tm+mt
source-git-commit: 7d61a6cd8cb2c381f85a19d9ccac3d235ffceaf1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Carregar um recurso de mídia no MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido.

1. Configure o item reproduzível do seu `MediaPlayer` objeto com o novo recurso a ser reproduzido.

   Substitua o item que pode ser reproduzido no momento de seu `MediaPlayer` objeto existente chamando `replaceCurrentResource` e transmitindo uma `MediaResource` instância existente.

1. Aguarde o TVSDK do navegador ser despachado `AdobePSDK.MediaPlayerStatusChangeEvent` com `event.status` um dos seguintes itens:

   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.ERROR`

      Por meio desses eventos, o objeto MediaPlayer notifica seu aplicativo se o recurso de mídia foi carregado com êxito.

1. Quando o estado do player de mídia mudar para `MediaPlayerStatus.INITIALIZED`, você poderá chamar `MediaPlayer.prepareToPlay`.

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamar `prepareToPlay` os start de resolução e processo de colocação de anúncios, se houver.
1. Quando o TVSDK do navegador despacha o `MediaPlayerStatus.PREPARED` evento, o fluxo de mídia foi carregado com êxito (um MediaPlayerItem é criado) e está preparado para reprodução.

Se ocorrer uma falha, o `MediaPlayer` alterna para o `MediaPlayerStatus.ERROR`.

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
