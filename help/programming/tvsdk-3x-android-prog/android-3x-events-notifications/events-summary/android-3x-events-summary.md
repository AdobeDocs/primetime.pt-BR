---
description: Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, ouvindo os eventos despachados pelo TVSDK.
title: Resumo dos eventos do player do Primetime
exl-id: 3912f140-1600-41fb-9dc4-306646b7cd85
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Resumo dos eventos do player do Primetime {#primetime-player-events-summary}

Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, ouvindo os eventos despachados pelo TVSDK.

## Eventos {#events}

O TVSDK notifica quando eventos, aos quais seu aplicativo deve responder, ocorrem. Cada evento corresponde a uma classe de ouvinte, com um método de retorno de chamada que deve ser implementado.

>[!TIP]
>
>Os códigos de evento são as constantes do enum `MediaPlayerEvent`.

`AdBreakCompletedEventListener`

* **** Isso significa que a reprodução do ad break está concluída.

* **Retorno de chamada para implementação** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** Isso significa que um ad break foi ignorado durante a reprodução.

* **Retorno de chamada para implementação** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **** Isso significa que a reprodução do ad break foi iniciada.

* **Retorno de chamada para implementação** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_START`

`AdClickedEventListener`

* **** Isso significa que um anúncio foi clicado durante a reprodução.

* **Retorno de chamada para implementação** `onAdClicked(AdClickEvent event)`
* **Código do evento** `AD_CLICK`

`AdCompletedEventListener`

* **** Isso significa que a reprodução do anúncio foi concluída.

* **Retorno de chamada para implementação** `onAdCompleted(AdPlaybackEvent event)`

* **Código do evento** `AD_COMPLETE`

`AdProgressEventListener`

* **** Significado: progresso dos relatórios durante a reprodução.

* **Retorno de chamada para implementação** `onAdProgress(AdPlaybackEvent event)`

* **Código do evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** Significa que a decisão do anúncio do Primetime foi concluída. Esse evento é aplicável somente ao conteúdo VOD.

* **Retorno de chamada para implementação** `onAdResolutionComplete()`

* **Código do evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** Isso significa que a reprodução do anúncio foi iniciada.

* **Retorno de chamada para implementação** `onAdStarted(AdPlaybackEvent event)`

* **Código do evento** `AD_START`

`AudioUpdatedEventListener`

* **** Isso significa que uma nova faixa de áudio foi detectada.

* **Retorno de chamada para implementação** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** Isso significa que o reprodutor iniciou o buffering.

* **Retorno de chamada para implementação** `onBufferingBegin(BufferEvent event)`

* **Código do evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** Isso significa que o reprodutor interrompeu o buffer.

* **Retorno de chamada para implementação** `onBufferingEnd(BufferEvent event)`

* **Código do evento** `BUFFERING_END`

`BufferPreparedEventListener`

* **** Isso significa que o buffer está preparado.

* **Retorno de chamada para implementação** `onBufferPrepared()`

* **Código do evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** Isso significa que um novo rastreamento de legenda foi detectado.

* **Retorno de chamada para implementação** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** Isso significa que novos metadados de DRM foram detectados no fluxo de mídia.

* **Retorno de chamada para implementação** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Código do evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **** Isso significa que um novo item de reprodutor de mídia foi criado.

* **Retorno de chamada para implementação** `onItemCreated(MediaPlayerItemEvent event)`

* **Código do evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** Significado: novas informações de carregamento foram criadas para o item atual.

* **Retorno de chamada para implementação** `onLoadComplete(MediaPlayerItemEvent event)`

* **Código do evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** Isso significa que um novo segmento foi carregado.

* **Retorno de chamada para implementação** `onLoadInformation(LoadInformationEvent event)`

* **Código do evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** Isso significa que o manifesto ou a lista de reprodução principal foi atualizada.

* **Retorno de chamada para implementação** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** Significado: falha na operação.

* **Retorno de chamada para implementação** `onNotification(NotificationEvent event)`

* **Código do evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** Isso significa que o intervalo de reprodução foi atualizado.

* **Retorno de chamada para implementação** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** Isso significa que uma nova taxa de reprodução é visível na tela.

* **Retorno de chamada para implementação** `onRatePlaying(PlaybackRateEvent event)`

* **Código do evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** Isso significa que o atributo de taxa do MediaPlayer foi definido.

* **Retorno de chamada para implementação** `onRateSelected(PlaybackRateEvent event)`

* **Código do evento** `RATE_SELECTED`

`PlayStartEventListener`

* **** Isso significa que a reprodução foi iniciada.

* **Retorno de chamada para implementação** `onPlayStart()`

* **Código do evento** `PLAY_START`

`ProfileChangeEventListener`

* **** Isso significa que o perfil atual do MediaPlayer foi alterado.

* **Retorno de chamada para implementação** `onProfileChanged(ProfileEvent event)`

* **Código do evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** Significado: a reprodução atingiu uma reserva de linha do tempo.

* **Retorno de chamada para implementação** `onReservationReached(ReservationEvent event)`

* **Código do evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **** Operação SignificadoSeek iniciada.

* **Retorno de chamada para implementação** `onSeekBegin(SeekEvent event)`

* **Código do evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **** Significado: a operação de busca foi concluída.

* **Retorno de chamada para implementação** `onSeekEnd(SeekEvent event)`

* **Código do evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **** Isso significa que a posição da busca foi ajustada devido às regras de reprodução interna ou às regras comerciais externas.

* **Retorno de chamada para implementação** `onPositionAdjusted(SeekEvent event)`

* **Código do evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** Significado: o tamanho da mídia está disponível.

* **Retorno de chamada para implementação** `onSizeAvailable(SizeAvailableEvent event)`

* **Código do evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** Isso significa que o estado do MediaPlayer foi alterado.

* **Retorno de chamada para implementação** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Código do evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** Isso significa que o indicador de reprodução foi alterado.

* **Retorno de chamada para implementação** `onTimeChanged(TimeChangeEvent event)`

* **Código do evento** `TIME_CHANGED`

`TimedEventEventListener`

* **** Significado: a operação é concluída com o tempo necessário para a operação.

* **Retorno de chamada para implementação** `onTimedEvent(TimedEventEvent event)`

* **Código do evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** Isso significa que novos metadados cronometrados foram adicionados a um item em segundo plano.

* **Retorno de chamada para implementação** `onTimedMetadata(TimedMetadataEvent event)`

* **Código do evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** Isso significa que novos metadados cronometrados foram detectados no fluxo de mídia.

* **Retorno de chamada para implementação** `onTimedMetadata(TimedMetadataEvent event)`

* **Código do evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** Isso significa que a linha do tempo foi modificada. Os anúncios podem ter sido adicionados ou removidos da linha do tempo.

* **Retorno de chamada para implementação** `onTimelineUpdated(TimelineEvent event)`

* **Código do evento** `TIMELINE_UPDATED`
