---
description: Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.
title: Salvar a posição do vídeo e retomar mais tarde
exl-id: 6b1eeeeb-ae13-437f-80cc-1ceb7bf8ac19
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Salvar a posição do vídeo e retomar mais tarde {#save-the-video-position-and-resume-later}

Você pode salvar a posição de reprodução atual em um vídeo e retomar a reprodução na mesma posição em uma sessão futura.

Os anúncios inseridos dinamicamente diferem entre as sessões do usuário, portanto, salvar a posição **com** anúncios em spliced refere-se a uma posição diferente em uma sessão futura. O TVSDK fornece métodos para recuperar a posição de reprodução, ignorando anúncios empacotados.

1. Quando o usuário sai de um vídeo, o aplicativo recupera e salva a posição no vídeo.

   >[!TIP]
   >
   >A duração do anúncio não está incluída.

   Os ad breaks podem variar em cada sessão devido a padrões de anúncios, limite de frequência e assim por diante. A hora atual do vídeo em uma sessão pode ser diferente em uma sessão futura. Ao salvar uma posição no vídeo, o aplicativo recupera a hora local, que pode ser salva no dispositivo ou em um banco de dados no servidor.

   Por exemplo, se o usuário estiver no 20º minuto do vídeo e essa posição incluir cinco minutos de anúncios, `getCurrentTime` retornará 1200 segundos, enquanto `getLocalTime` nesta posição retornará 900 segundos.

   >[!IMPORTANT]
   >
   >A hora local e a hora atual são as mesmas para fluxos ao vivo/lineares. Nesse caso, `convertToLocalTime` não tem efeito. Para VOD, a hora local permanece inalterada durante a reprodução dos anúncios.

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

   * Para retomar a reprodução do vídeo a partir da posição salva em uma sessão anterior, use `seekToLocalTime`.

      >[!TIP]
      >
      >Esse método é chamado somente com valores de hora locais. Se o método for chamado com os resultados da hora atual, ocorrerá um comportamento incorreto.

   * Para buscar o horário atual, use `seek`.

1. Quando o aplicativo recebe a variável `onStatusChanged` evento de alteração de status, procure a hora local salva.

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

1. Forneça os ad breaks de acordo com as especificações da interface de política de anúncios.
1. Implemente um seletor de política de anúncios personalizado estendendo o seletor de política de anúncios padrão.
1. Fornecer os ad breaks que devem ser apresentados ao usuário implementando `selectAdBreaksToPlay`.

   Esse método inclui um ad break precedente e ad breaks intermediários antes da posição da hora local. Seu aplicativo pode decidir reproduzir um ad break precedente e retomar o horário local especificado, reproduzir um ad break intermediário e retomar o horário local especificado ou não reproduzir ad breaks.
