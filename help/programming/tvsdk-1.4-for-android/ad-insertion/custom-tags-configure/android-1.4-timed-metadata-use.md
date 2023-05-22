---
description: Você pode usar TimedMetadata quando a hora atual da reprodução corresponder à hora inicial.
title: Usar metadados cronometrados
exl-id: 7f87cd14-121a-4543-ab0a-a03d829d040b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Usar metadados cronometrados {#use-timed-metadata}

Você pode usar TimedMetadata quando a hora atual da reprodução corresponder à hora inicial.

Para usar essas `TimedMetadata` objetos durante a reprodução, use a variável `ArrayList` de [Armazenar objetos de metadados cronometrados conforme são despachados](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Execute um cronômetro e consulte repetidamente a hora de reprodução atual.
1. Localizar todos os `TimedMetadata` objetos com horas de início que correspondem à hora de reprodução atual.

   Você pode usar esses objetos para concluir várias ações.

   >[!IMPORTANT]
   >
   >Ao verificar se o tempo de reprodução atual corresponde a algum `TimedMetadata` objetos, incluir `shouldTriggerSubscribedTagEvent` como condição.

   A linha do tempo pode mudar como resultado de vários comportamentos de anúncios. Por exemplo, um ou mais ad breaks podem ser movidos de suas posições originais na linha do tempo, mas `shouldTriggerSubscribedTagEvent` assegura que a `TimeMetadata` a hora de início do objeto corresponde à hora de reprodução atual.

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

1. Liberar periodicamente arquivos obsoletos `TimedMetadata` instâncias da lista para evitar que a memória cresça continuamente.
