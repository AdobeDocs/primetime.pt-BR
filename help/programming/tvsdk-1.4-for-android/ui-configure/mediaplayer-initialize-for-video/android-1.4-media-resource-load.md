---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.
title: Carregar um recurso de mídia no MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---


# Carregar um recurso de mídia no MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.

1. Defina o item reproduzível do MediaPlayer com o novo recurso a ser reproduzido.

   Substitua o item do MediaPlayer atual, chamando `MediaPlayer.replaceCurrentItem` e passando uma instância `MediaResource` existente.

1. Registre uma implementação da interface `MediaPlayer.PlaybackEventListener` com a instância `MediaPlayer`.

   * `onPrepared`
   * `onStateChanged`e verifique se INICIALIZADO e ERRO.

1. Quando o estado do reprodutor de mídia é alterado para INICIALIZADO, você pode chamar `MediaPlayer.prepareToPlay`

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamar `prepareToPlay` inicia a resolução e o processo de posicionamento do anúncio, se houver.

1. Quando o TVSDK chama o retorno de chamada `onPrepared`, o fluxo de mídia é carregado com êxito e está preparado para reprodução.

   Quando o fluxo de mídia é carregado, um `MediaPlayerItem` é criado.

>Se ocorrer uma falha, o `MediaPlayer` alterna para o status ERROR. Ele também notifica seu aplicativo, chamando seu retorno de chamada `PlaybackEventListener.onStateChanged`.
>
>Isso passa por vários parâmetros:
>* Um parâmetro `state` do tipo `MediaPlayer.PlayerState` com o valor `MediaPlayer.PlayerState.ERROR`.
   >
   >
* Um parâmetro `notification` do tipo `MediaPlayerNotification` que contém informações de diagnóstico sobre o evento de erro.


O código de amostra simplificado a seguir ilustra o processo de carregamento de um recurso de mídia:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer  
instancemediaPlayer.addEventListener( 
  MediaPlayer.Event.PLAYBACK, 
  new MediaPlayer.PlaybackEventListener()) { 
    @Overridepublic void onPrepared() { 
        // at this point, the resource is successfully loaded and available 
        // and the MediaPlayer is ready to start the playback 
        // once the resource is loaded, the MediaPlayer is able to 
        // provide a reference to the current "playable item" 
 
        MediaPlayerItem playerItem = mediaPlayer.CurrentItem(); 
 
        if (playerItem != null) {     
            // here we can take a look at the properties of the     
            // loaded stream 
        } 
    } @Overridepublic void onStateChanged( 
        MediaPlayer.PlayerState state,  
        MediaPlayerNotification notification) { 
        if (state == MediaPlayer.PlayerState.ERROR) { 
            // something bad happened - the resource cannot be loaded    
            // details about the problem are provided via the  
            // MediaPlayerNotification instance 
        }  
        elseif (state == MediaPlayer.PlayerState.INITIALIZED) {     
            mediaPlayer.prepareToPlay(); 
        } 
    } 
    // implementation of the other methods in the PlaybackEventListener interface... 
} 
```
