---
description: Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.
title: Carregar um recurso de mídia no reprodutor de mídia
exl-id: ee11876b-c752-46cc-8e65-8c1608a41362
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Carregar um recurso de mídia no reprodutor de mídia {#load-a-media-resource-in-the-media-player}

Carregue um recurso instanciando diretamente um MediaResource e carregando o conteúdo de vídeo a ser reproduzido. Essa é uma maneira de carregar um recurso de mídia.

1. Defina o reprodutor de mídia para reproduzir o novo recurso.

   Substituir o item reproduzível no momento chamando `MediaPlayer.replaceCurrentResource()` e transmitindo um existente `MediaResource` instância.

   Isso inicia o processo de carregamento de recursos.

1. Registre o `MediaPlayerEvent.STATUS_CHANGED` evento com o `MediaPlayer` instância. No retorno de chamada, verifique pelo menos os seguintes valores de status:

   * `MediaPlayerStatus.PREPARED`
   * `MediaPlayerStatus.INITIALIZED`
   * `MediaPlayerStatus.ERROR`

   Através destes eventos, a `MediaPlayer` O objeto notifica o aplicativo quando carregou o recurso de mídia com êxito.
1. Quando o status do reprodutor de mídia muda para `INITIALIZED`, você pode chamar `MediaPlayer.prepareToPlay()`.

   Esse status indica que a mídia foi carregada com sucesso. O novo `MediaPlayerItem` está pronto para reprodução. Chamando `prepareToPlay()` inicia o processo de resolução e posicionamento do anúncio, se houver.

Se ocorrer uma falha, o reprodutor de mídia alterna para o `ERROR` status.

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
