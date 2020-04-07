---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.
seo-description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.
seo-title: Carregar um recurso de mídia no player de mídia
title: Carregar um recurso de mídia no player de mídia
uuid: 0334fa69-1d92-44d8-8891-2bc90a1ea498
translation-type: tm+mt
source-git-commit: 67975894814fbed8cfc49764a54b80d123032a49

---


# Carregar um recurso de mídia no player de mídia {#load-a-media-resource-in-the-media-player}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Esta é uma maneira de carregar um recurso de mídia.

1. Defina o player de mídia para reproduzir o novo recurso.

   Substitua o item que pode ser reproduzido no momento chamando `MediaPlayer.replaceCurrentResource()` e transmitindo uma `MediaResource` instância existente.

   Isso start o processo de carregamento de recursos.

1. Registre o `MediaPlayerEvent.STATUS_CHANGED` evento com a `MediaPlayer` instância. Na chamada de retorno, verifique pelo menos os seguintes valores de status:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`
   Por meio desses eventos, o `MediaPlayer` objeto notifica seu aplicativo quando ele carregou com êxito o recurso de mídia.
1. Quando o status do player de mídia mudar para `INITIALIZED`, você poderá chamar `MediaPlayer.prepareToPlay()`.

   Esse status indica que a mídia foi carregada com êxito. O novo `MediaPlayerItem` está pronto para reprodução. Chamar `prepareToPlay()` os start de resolução e processo de colocação de anúncios, se houver.

Se ocorrer uma falha, o player de mídia alterna para o `ERROR` status.

O código de amostra simplificado a seguir ilustra o processo de carregamento de um recurso de mídia:

```java
// mediaResource is a properly configured MediaResource instance 
// mediaPlayer is a MediaPlayer instance 
// register a PlaybackEventListener implementation with the MediaPlayer instance 
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatus status) { 
        if(event.getStatus() == MediaPlayerStatus.PREPARED) { 
            // The resource is successfully loaded and available. The  
            // MediaPlayer is ready to start the playback and can 
            // provide a reference to the current playable item 
            MediaPlayerItem playerItem = mediaPlayer.getCurrentItem(); 
            if (playerItem != null) { 
                // We can look at the properties of the loaded stream 
            } 
        } 
        else if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            //Something bad happened - the resource cannot be loaded. 
            // The Metadata object in the event provides details. 
        } 
        else if (status == MediaPlayerStatus.INITIALIZED) { 
            mediaPlayer.prepareToPlay(); 
        } 
    } 
} 
```
