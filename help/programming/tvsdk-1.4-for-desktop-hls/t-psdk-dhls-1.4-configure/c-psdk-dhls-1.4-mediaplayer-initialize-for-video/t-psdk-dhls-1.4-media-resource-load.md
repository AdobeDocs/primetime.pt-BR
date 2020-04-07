---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.
seo-description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.
seo-title: Carregar um recurso de mídia no MediaPlayer
title: Carregar um recurso de mídia no MediaPlayer
uuid: 8af3e8d1-359d-483c-b394-b95054f7265a
translation-type: tm+mt
source-git-commit: 84924d84bfa436a8807c2e8d74d1dc268d457051

---


# Carregar um recurso de mídia no MediaPlayer{#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.

1. Configure o item reproduzível do seu `MediaPlayer` objeto com o novo recurso a ser reproduzido.

   Substitua o item reproduzível atual do MediaPlayer chamando `MediaPlayer.replaceCurrentResource` e transmitindo uma `MediaResource` instância existente.

1. Verifique pelo menos as seguintes alterações:

   * INICIALIZADO
   * PREPARADO
   * ERRO

      Por meio desses eventos, o `MediaPlayer` objeto pode notificar seu aplicativo quando o recurso de mídia for carregado com êxito.

1. Quando o estado do player de mídia mudar para INICIALIZADO, você pode chamar `MediaPlayer.prepareToPlay`

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamar `prepareToPlay` os start de resolução e processo de colocação de anúncios, se houver.

1. Quando o status do player de mídia é alterado para PREPARADO, o fluxo de mídia é carregado com êxito e está preparado para a reprodução.

   Quando o fluxo de mídia é carregado, um `MediaPlayerItem` é criado.

Se ocorrer uma falha, o MediaPlayer alterna para o status ERROR. Ele também notifica seu aplicativo enviando o `STATUS_CHANGED` evento para seu `MediaPlayerStatusChangeEvent` retorno de chamada.

Isso passa por vários parâmetros:
* Um `type` parâmetro do tipo string com o valor `ERROR`.

* Um `MediaError` parâmetro que pode ser usado para obter uma notificação que contém informações de diagnóstico sobre o evento error.


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
