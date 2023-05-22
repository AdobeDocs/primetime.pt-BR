---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.
title: Carregar um recurso de mídia no MediaPlayer
exl-id: 8258c45e-f8bf-434d-9621-88c189e1530d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Carregar um recurso de mídia no MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.

1. Defina seu `MediaPlayer` item reproduzível do objeto com o novo recurso a ser reproduzido.

   Substitua o item reproduzível atual do MediaPlayer chamando `MediaPlayer.replaceCurrentResource` e transmitindo um existente `MediaResource` instância.

1. Verifique pelo menos as seguintes alterações:

   * INICIALIZADO
   * PREPARADO
   * ERRO

      Através destes eventos, a `MediaPlayer` O objeto pode notificar seu aplicativo quando o recurso de mídia é carregado com êxito.

1. Quando o estado do reprodutor de mídia muda para INITIALIZED, você pode chamar `MediaPlayer.prepareToPlay`

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamando `prepareToPlay` inicia o processo de resolução e posicionamento do anúncio, se houver.

1. Quando o status do reprodutor de mídia é alterado para PREPARADO, o fluxo de mídia é carregado com êxito e está preparado para reprodução.

   Quando o fluxo de mídia é carregado, uma variável `MediaPlayerItem` é criado.

Se ocorrer uma falha, o MediaPlayer alterna para o status ERRO. Ele também notifica seu aplicativo enviando o `STATUS_CHANGED` para o seu `MediaPlayerStatusChangeEvent` retorno de chamada.

Isso passa vários parâmetros:
* A `type` parâmetro do tipo string com o valor `ERROR`.

* A `MediaError` parâmetro que você pode usar para obter uma notificação que contém informações de diagnóstico sobre o evento de erro.


<!--<a id="example_3774607C6F08473282CF0CB7F3D82373"></a>-->

O código de amostra simplificado a seguir ilustra o processo de carregamento de um recurso de mídia:

```
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register an event listener with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
private function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
   switch(event.status) { 
      case MediaPlayerStatus.INITIALIZED: 
          // at this point, the resource is successfully loaded 
          // the media player will provide a reference to the current 
          // "playable item" ( is guarantee to be valid and not-null). 
          var playerItem: MediaPlayerItem = mediaPlayer.currentItem; 
          // we can take a look at the media item characteristics like 
          // alternate audio tracks, profile information, if is a live stream 
          // if is drm protected 
          mediaPlayer.prepareToPlay(); 
          break; 
    case MediaPlayerStatus.PREPARED: 
         // at this point, the resource is successfully processed all  
         // advertisement placements have been executed and the the  
         // MediaPlayer is ready to start the playback 
        if (autoPlay) { 
            mediaPlayer.play(); 
        } 
        break; 
    case MediaPlayerStatus.ERROR: 
        // something bad happened - the resource cannot be loaded 
        // details about the problem are provided via the event.error property 
        break; 
        // implementation of the other methods in the PlaybackEventListener interface 
        ... 
    } 
}
```
