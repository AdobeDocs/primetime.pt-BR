---
description: Você pode usar TimedMetadata quando a hora de reprodução atual corresponde à hora de início.
title: Usar metadados cronometrados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 1%

---


# Usar metadados cronometrados {#use-timed-metadata}

Você pode usar TimedMetadata quando a hora de reprodução atual corresponde à hora de início.

Para usar esses objetos `TimedMetadata` salvos durante a reprodução, use o `ArrayList` salvo de [Armazenar objetos de metadados cronometrados, pois são despachados](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Execute um temporizador e consulte repetidamente o tempo de reprodução atual.
1. Encontre todos os objetos `TimedMetadata` com horários de início que correspondem ao tempo de reprodução atual.

   É possível usar esses objetos para concluir várias ações.

   >[!IMPORTANT]
   >
   >Ao verificar se o tempo de reprodução atual corresponde a qualquer objeto `TimedMetadata` , inclua `shouldTriggerSubscribedTagEvent` como uma condição.

   A linha do tempo pode mudar como resultado de vários comportamentos de publicidade. Por exemplo, uma ou mais quebras de anúncio podem ser movidas de suas posições originais na linha do tempo, mas `shouldTriggerSubscribedTagEvent` garante que a hora de início do objeto `TimeMetadata` corresponda ao tempo de reprodução atual.

   Por exemplo:

   ```java
    _playbackClockEventListener = new Clock.ClockEventListener() {
       @Override
       public void onTick(String name) {
           getActivity().runOnUiThread(new Runnable() {
               @Override
               public void run() {
                   /* handle timedmetadata object list  */ 
                   if (_mediaPlayer != null && _timedMetadataList != null && _timedMetadataList.size() > 0) {
                       if (_lastKnownStatus == MediaPlayer.PlayerState.PLAYING) {
                           long localTime = _mediaPlayer.getLocalTime();
                           Iterator<TimedMetadata> iterator = _timedMetadataList.iterator(); 
                           while (iterator.hasNext()) {
                               TimedMetadata timedMetadata = iterator.next();
                               long diff = localTime - timedMetadata.getTime();
                               if (diff >= 0 &&
                                   diff <= PLAYBACK_CLOCK_INTERVAL &&
                                   _mediaPlayer.shouldTriggerSubscribedTagEvent()) {
                                   // use timed metadata object
                               }
                           }
                       }
                   }
               }
           });
       }
   };
   _playbackClock.addClockEventListener(_playbackClockEventListener);
   ```

1. Limpe periodicamente instâncias obsoletas `TimedMetadata` da lista para evitar que a memória cresça continuamente.