---
description: Crie um PlaybackManager que gerencia a configuração e a operação de reprodução do fluxo HLS. Nenhuma outra configuração é necessária.
seo-description: Crie um PlaybackManager que gerencia a configuração e a operação de reprodução do fluxo HLS. Nenhuma outra configuração é necessária.
seo-title: Ativar reprodução de vídeo
title: Ativar reprodução de vídeo
uuid: ddc0defa-c40f-4ee6-a69f-d5eeca6c2fce
translation-type: tm+mt
source-git-commit: a33e1f290fcf78e6f131910f6037f4803f7be98d
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 0%

---


# Habilitar reprodução de vídeo {#enable-video-playback}

Crie um PlaybackManager que gerencia a configuração e a operação de reprodução do fluxo HLS. Nenhuma outra configuração é necessária.

1. Crie o objeto do player de mídia verificando se o seguinte código existe em [!DNL PlayerFragment.java]:

   ```java
   private MediaPlayer createMediaPlayer() { 
           MediaPlayer mediaPlayer = DefaultMediaPlayer.create(getActivity().getApplicationContext()); 
           return mediaPlayer;
   ```

   <!-- I've duplicated this information. It also exists in the PlayerFragment section, just before the Feature manager section. I figured that I should have it here as well, in case they jump directly to this section.-->

1. Crie o gerenciador de reprodução por meio de `ManagerFactory`:

   ```java
   playbackManager = ManagerFactory.getPlaybackManager(config, mediaPlayer);
   ```

1. Implemente `PlaybackManagerEventListener` em `PlayerFragment` para manipular os eventos de reprodução:

   ```java
   private final PlaybackManagerEventListener playbackManagerEventListener =  
     new PlaybackManagerEventListener() 
   ```

1. Registre o ouvinte do evento em `PlayerFragment`:

   ```
   playbackManager.addEventListener(playbackManagerEventListener);
   ```

1. Configure o recurso de vídeo:

   ```
   playbackManager.setupVideo(url, adsManager); 
   ```

1. Configure as operações da barra de controle em `PlayerFragment`:

   ```
   controlBar.pressPlay() { 
       playbackManager.play();  
   }
   ```

## Documentação da API relacionada {#related-api-documentation}

* [Class PlaybackManager](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.html)
* [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html)
* [mediacore.utils.TimeRange](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/utils/TimeRange.html)
* [mediacore.BufferControlParameters](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/BufferControlParameters.html)
* [mediacore.MediaPlayer.PlayerState](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/com/adobe/mediacore/MediaPlayer.PlayerState.html)