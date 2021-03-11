---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.
title: Carregar um recurso de mídia no MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---


# Carregar um recurso de mídia no MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.

1. Defina o item reproduzível do objeto `MediaPlayer` com o novo recurso a ser reproduzido.

   Substitua o item do MediaPlayer atual, chamando `MediaPlayer.replaceCurrentResource` e passando uma instância `MediaResource` existente.

1. Verifique pelo menos as seguintes alterações:

   * INICIALIZADO
   * PREPARADO
   * ERRO

      Por meio desses eventos, o objeto `MediaPlayer` pode notificar seu aplicativo quando o recurso de mídia for carregado com êxito.

1. Quando o estado do reprodutor de mídia é alterado para INICIALIZADO, você pode chamar `MediaPlayer.prepareToPlay`

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamar `prepareToPlay` inicia a resolução e o processo de posicionamento do anúncio, se houver.

1. Quando o status do reprodutor de mídia é alterado para PREPARED, o fluxo de mídia é carregado com êxito e está preparado para reprodução.

   Quando o fluxo de mídia é carregado, um `MediaPlayerItem` é criado.

Se ocorrer uma falha, o MediaPlayer alterna para o status ERROR. Ele também notifica seu aplicativo, despachando o evento `STATUS_CHANGED` para seu retorno de chamada `MediaPlayerStatusChangeEvent`.

Isso passa por vários parâmetros:
* Um parâmetro `type` do tipo string com o valor `ERROR`.

* Um parâmetro `MediaError` que pode ser usado para obter uma notificação que contém informações de diagnóstico sobre o evento de erro.


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
