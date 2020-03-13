---
description: Quando um usuário clica em um anúncio, seu aplicativo deve pausar a reprodução do conteúdo principal do vídeo.
seo-description: Quando um usuário clica em um anúncio, seu aplicativo deve pausar a reprodução do conteúdo principal do vídeo.
seo-title: Pausar e retomar a reprodução
title: Pausar e retomar a reprodução
uuid: a8fec392-3a71-4086-abf1-23522d023680
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Pausar e retomar a reprodução {#pause-and-resume-playback}

Quando um usuário clica em um anúncio, seu aplicativo deve pausar a reprodução do conteúdo principal do vídeo.

Substitua a atividade `onPause` e `onResume` da atividade do Android.

```java
@Override 
public void onResume() { 
    super.onResume(); 
    requestAudioFocus(); 
    if (_lastKnownStatus == MediaPlayer.PlayerState.PAUSED) { 
        _mediaPlayer.play(); 
    } 
} 
... 
 
@Override 
public void onPause() { 
    super.onPause(); 
    if (_mediaPlayer != null) { 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING || 
          _mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) { 
            _savedPlayerState = _mediaPlayer.getStatus(); 
            _lastKnownTime = _mediaPlayer.getCurrentTime(); 
        } 
        if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PLAYING) { 
            _mediaPlayer.pause(); 
            _lastKnownStatus = MediaPlayer.PlayerState.PAUSED; 
        } 
    } 
} 
 
abandonAudioFocus(); 
```

