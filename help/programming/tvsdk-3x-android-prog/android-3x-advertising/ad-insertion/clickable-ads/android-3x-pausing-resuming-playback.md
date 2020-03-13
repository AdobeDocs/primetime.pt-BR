---
description: Quando um usuário clica em um anúncio, seu aplicativo deve pausar a reprodução do conteúdo principal do vídeo.
seo-description: Quando um usuário clica em um anúncio, seu aplicativo deve pausar a reprodução do conteúdo principal do vídeo.
seo-title: Pausar e retomar a reprodução
title: Pausar e retomar a reprodução
uuid: 87ba9f05-912d-4b85-8add-feb26a796a3a
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Pausar e retomar a reprodução {#pause-and-resume-playback}

Quando um usuário clica em um anúncio, seu aplicativo deve pausar a reprodução do conteúdo principal do vídeo.

1. Substitua as atividades `onPause` e `onResume` do Android.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       requestAudioFocus(); 
       if (_lastKnownStatus == MediaPlayerStatus.PAUSED) { 
           _mediaPlayer.play(); 
       } 
   } 
   ... 
   
   @Override 
   public void onPause() { 
       super.onPause(); 
       if (_mediaPlayer != null) { 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING || 
             _mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) { 
               _savedPlayerStatus = _mediaPlayer.getStatus(); 
               _lastKnownTime = _mediaPlayer.getCurrentTime(); 
           } 
           if (_mediaPlayer.getStatus() == MediaPlayerStatus.PLAYING) { 
               _mediaPlayer.pause(); 
               _lastKnownStatus = MediaPlayerStatus.PAUSED; 
           } 
       } 
   } 
   abandonAudioFocus(); 
   ```

