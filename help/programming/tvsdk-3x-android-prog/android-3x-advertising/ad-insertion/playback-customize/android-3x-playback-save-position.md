---
description: Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.
seo-description: Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.
seo-title: Salve a posição do vídeo e retome mais tarde
title: Salve a posição do vídeo e retome mais tarde
uuid: cff1715e-c7a9-4eda-ad71-31892c3c1e78
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Salve a posição do vídeo e retome mais tarde {#save-the-video-position-and-resume-later}

Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

As publicidades inseridas dinamicamente diferem entre as sessões do usuário, portanto, salvar a posição **com** publicidades em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição de reprodução ao ignorar anúncios segmentados.

1. Quando o usuário sai de um vídeo, seu aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >A duração do anúncio não está incluída.

   As quebras de anúncios podem variar em cada sessão devido aos padrões de anúncios, limitação de frequência e assim por diante. A hora atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local, que você pode salvar no dispositivo ou em um banco de dados no servidor.

   Por exemplo, se o usuário estiver no 20º minuto do vídeo e essa posição incluir cinco minutos de anúncios, `getCurrentTime` retornará 1200 segundos, enquanto `getLocalTime` nessa posição retornará 900 segundos.

   >[!IMPORTANT]
   >
   >A hora local e a hora atual são as mesmas para fluxos ao vivo/lineares. Neste caso, não `convertToLocalTime` tem efeito. Para VOD, o tempo local permanece inalterado enquanto os anúncios são reproduzidos.

   ```java
   // Save the user session when player activity stops 
       @Override 
       public void onStop(){ 
           super.onStop(); 
           ... 
           prefs = PreferenceManager.getDefaultSharedPreferences( 
                                     getActivity().getApplicationContext()); 
           SharedPreferences.Editor editor = prefs.edit(); 
           // get the local time where stream stopped playing and  
           // save it in System preferences 
           editor.putLong(LAST_LOCAL_TIME, _mediaPlayer.getLocalTime());  
           editor.putString(LAST_MEDIA_RESOURCE, _contentInfo.toMediaResource().getUrl()); 
           editor.commit(); 
           ... 
       }
   ```

1. Restaure a sessão do usuário quando a atividade do player for retomada.

   ```java
   @Override 
   public void onResume() { 
       super.onResume(); 
       ... 
       prefs =  
         PreferenceManager.getDefaultSharedPreferences(getActivity().getApplicationContext()); 
       if (prefs.getString(LAST_MEDIA_RESOURCE, "nil"). 
         equals(_contentInfo.toMediaResource().getUrl())) { 
           _lastKnownLocalTime =  
             prefs.getLong(LAST_LOCAL_TIME, 0); // get the last local time  
                                                // saved in system preferences 
           if(_lastKnownLocalTime > 0) { 
               _shouldResumePlayback = true; 
           } 
       } 
       ... 
   } 
   ```

1. Para retomar o vídeo na mesma posição:

   * Para retomar a reprodução do vídeo da posição que foi salva de uma sessão anterior, use `seekToLocalTime`.

      >[!TIP]
      >
      >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados de tempo atuais, ocorrerá comportamento incorreto.

   * Para buscar o horário atual, use `seek`.

1. Quando o aplicativo receber o evento de alteração de `onStatusChanged` status, procure a hora local salva.

   ```java
   private final MediaPlayer.PlaybackEventListener _playbackEventListener =  
     new MediaPlayer.PlaybackEventListener() { 
       @Override 
       public void onPrepared() { 
           ... 
           if(_shouldResumePlayback){ 
               if(_lastKnownLocalTime >= 0) { 
                    _mediaPlayer.seekToLocalTime(_lastKnownLocalTime); 
               } 
           } 
           ... 
       } 
       ... 
   }
   ```

1. Forneça os intervalos de anúncio conforme especificado na interface da política de anúncios.
1. Implemente um seletor de política de publicidade personalizado estendendo o seletor de política de publicidade padrão.
1. Forneça as pausas de anúncio que devem ser apresentadas ao usuário por meio da implementação `selectAdBreaksToPlay`.

   Esse método inclui uma pausa de anúncio precedente e uma pausa de anúncio intermediário antes da posição de hora local. Seu aplicativo pode decidir reproduzir um intervalo de anúncios precedente e retomar para o horário local especificado, reproduzir um intervalo de anúncios intermediário e retomar para o horário local especificado, ou não reproduzir nenhum intervalo de anúncios.