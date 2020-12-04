---
seo-title: Ativar áudio de fundo
title: Ativar áudio de fundo
uuid: aa6dc934-e85c-4db1-901b-9777f47106e6
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '63'
ht-degree: 0%

---


# Ativar áudio de fundo {#enable-background-audio}

Para habilitar a reprodução de áudio quando o aplicativo estiver em segundo plano, o aplicativo deve chamar `enableAudioPlaybackInBackground` a API do MediaPlayer com true como argumento quando o player estiver no estado PREPARADO.

```
_mediaPlayer.enableAudioPlaybackInBackground(true);
```

O aplicativo deve pausar a reprodução quando perde o foco de áudio durante eventos como responder ao telefone, etc. O trecho de código a seguir demonstra como implementar o `OnAudioFocusChangeListener`:

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
