---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.
seo-description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.
seo-title: Carregar um recurso de mídia no MediaPlayer
title: Carregar um recurso de mídia no MediaPlayer
uuid: 6ee8032f-0728-423f-a1d2-5030aa7db14f
translation-type: tm+mt
source-git-commit: 4ef05be045334a2e723da4c7c6a7ee22fb0f776c
workflow-type: tm+mt
source-wordcount: '252'
ht-degree: 0%

---


# Carregue um recurso de mídia no MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.

1. Defina o item reproduzível do MediaPlayer com o novo recurso a ser reproduzido.

   Substitua o item do MediaPlayer existente, que pode ser reproduzido, chamando `MediaPlayer.replaceCurrentItem` e transmitindo uma instância `MediaResource` existente.

1. Registre uma implementação da interface `MediaPlayer.PlaybackEventListener` com a instância `MediaPlayer`.

   * `onPrepared`
   * `onStateChanged`e verifique se INITIALIZED e ERROR (INICIALIZADO e ERRO).

1. Quando o estado do media player mudar para INICIALIZADO, você pode chamar `MediaPlayer.prepareToPlay`

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamar `prepareToPlay` start a resolução e o processo de colocação do anúncio, se houver.

1. Quando o TVSDK chama o retorno de chamada `onPrepared`, o fluxo de mídia foi carregado com êxito e está preparado para a reprodução.

   Quando o fluxo de mídia é carregado, um `MediaPlayerItem` é criado.

>Se ocorrer uma falha, o `MediaPlayer` alterna para o status ERROR. Ele também notifica seu aplicativo chamando seu `PlaybackEventListener.onStateChanged`retorno de chamada.
>
>Isso passa por vários parâmetros:
>* Um parâmetro `state` do tipo `MediaPlayer.PlayerState` com o valor de `MediaPlayer.PlayerState.ERROR`.
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
