---
description: Você pode usar TimedMetadata quando a hora de reprodução atual corresponder à hora de início.
seo-description: Você pode usar TimedMetadata quando a hora de reprodução atual corresponder à hora de início.
seo-title: Usar metadados cronometrados
title: Usar metadados cronometrados
uuid: 98bb8c08-2794-42d6-b5c3-b1047ac804fe
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Usar metadados cronometrados {#use-timed-metadata}

Você pode usar TimedMetadata quando a hora de reprodução atual corresponder à hora de início.

Para usar esses `TimedMetadata` objetos salvos durante a reprodução, use os objetos salvos `ArrayList` de metadados cronometrados da [Loja conforme são despachados](../../ad-insertion/custom-tags-configure/android-1.4-timed-metadata-store.md).

1. Execute um temporizador e consulte repetidamente o tempo de reprodução atual.
1. Encontre todos os `TimedMetadata` objetos com horas de início que correspondem à hora de reprodução atual.

   É possível usar esses objetos para concluir várias ações.

[!IMPORTANT]
Ao verificar se o tempo de reprodução atual corresponde a qualquer `TimedMetadata` objeto, inclua `shouldTriggerSubscribedTagEvent` como uma condição.

A linha do tempo pode mudar como resultado de vários comportamentos de anúncio. Por exemplo, uma ou mais quebras de anúncio podem ser movidas de suas posições originais na linha do tempo, mas `shouldTriggerSubscribedTagEvent` garante que a hora de início do `TimeMetadata` objeto corresponda à hora de reprodução atual.

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

1. Limpe periodicamente `TimedMetadata` instâncias obsoletas da lista para evitar que a memória cresça continuamente.