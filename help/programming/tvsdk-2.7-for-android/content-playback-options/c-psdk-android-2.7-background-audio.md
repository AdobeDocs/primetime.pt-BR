---
title: Habilitar áudio de plano de fundo
description: Habilitar áudio de plano de fundo
copied-description: true
exl-id: db494969-ef63-46ad-9f08-a95f58c8b27b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---

# Habilitar áudio de plano de fundo {#enable-background-audio}

Para habilitar a reprodução de áudio quando o aplicativo estiver em segundo plano, o aplicativo deve chamar `enableAudioPlaybackInBackground` API do MediaPlayer com verdadeiro como argumento quando o player está no estado PREPARADO.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

O aplicativo deve pausar a reprodução quando perder o controle sobre o foco de áudio durante eventos como responder ao telefone etc. O trecho de código a seguir demonstra como implementar o `OnAudioFocusChangeListener`:

```
/** 
 * Register the AudioFocus Change listener to track Audio focus from device. 
 */ 
 AudioManager.OnAudioFocusChangeListener onAudioFocusChangeListener = new AudioManager.OnAudioFocusChangeListener(){ 
     @Override 
     public void onAudioFocusChange(int focusChange){ 
          switch(focusChange){ 
               case AudioManager.AUDIOFOCUS_GAIN: 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT_CAN_DUCK: 
                    /* lower output volume*/ 
                    break; 
               case AudioManager.AUDIOFOCUS_LOSS: 
               case AudioManager.AUDIOFOCUS_LOSS_TRANSIENT: 
                    if(_lastKnownStatus ==MediaPlayerStatus.PLAYING) 
                         _mediaPlayer.pause(); 
                    break; 
          } 
     } 
}; 
 
AudioManager audioManager = (AudioManager) getActivity().getApplicationContext().getSystemService(Context.AUDIO_SERVICE); 
audioManager.requestAudioFocus(onAudioFocusChangeListener, AudioManager.STREAM_MUSIC, AudioManager.AUDIOFOCUS_GAIN);
```
