---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.
title: Carregar um recurso de mídia no MediaPlayer
exl-id: 2d5e95bc-3962-4356-b90f-e550066f7a70
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Carregar um recurso de mídia no MediaPlayer {#load-a-media-resource-in-the-mediaplayer}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.

1. Defina o item reproduzível do MediaPlayer com o novo recurso a ser reproduzido.

   Substitua o item reproduzível atual do MediaPlayer chamando `MediaPlayer.replaceCurrentItem` e transmitindo um existente `MediaResource` instância.

1. Registrar uma implementação do `MediaPlayer.PlaybackEventListener` com a `MediaPlayer` instância.

   * `onPrepared`
   * `onStateChanged`e verifique INITIALIZED e ERROR.

1. Quando o estado do reprodutor de mídia muda para INITIALIZED, você pode chamar `MediaPlayer.prepareToPlay`

   O estado INITIALIZED indica que a mídia foi carregada com êxito. Chamando `prepareToPlay` inicia o processo de resolução e posicionamento do anúncio, se houver.

1. Quando o TVSDK chama o `onPrepared` retorno de chamada, o fluxo de mídia foi carregado com sucesso e está preparado para reprodução.

   Quando o fluxo de mídia é carregado, uma variável `MediaPlayerItem` é criado.

>Se ocorrer uma falha, a variável `MediaPlayer` alterna para o status ERRO. Ele também notifica seu aplicativo, chamando seu `PlaybackEventListener.onStateChanged`retorno de chamada.
>
>Isso passa vários parâmetros:
>* A `state` parâmetro do tipo `MediaPlayer.PlayerState` com o valor de `MediaPlayer.PlayerState.ERROR`.
>
>* A `notification` parâmetro do tipo `MediaPlayerNotification` que contém informações de diagnóstico sobre o evento de erro.


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
