---
description: Seu aplicativo pode monitorar a atividade no reprodutor e a alteração do status do reprodutor ouvindo os eventos despachados pelo TVSDK.
title: Resumo de eventos do player do Primetime
exl-id: 3912f140-1600-41fb-9dc4-306646b7cd85
source-git-commit: 59f7f8aa82be59c4012ee80648032600590bc4e1
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Resumo de eventos do player do Primetime {#primetime-player-events-summary}

Seu aplicativo pode monitorar a atividade no reprodutor e a alteração do status do reprodutor ouvindo os eventos despachados pelo TVSDK.

## Eventos {#events}

O TVSDK notifica quando ocorrem eventos aos quais o aplicativo deve responder. Cada evento corresponde a uma classe de ouvinte, com um método de retorno de chamada que você deve implementar.

>[!TIP]
>
>Os códigos de evento são as constantes da variável `MediaPlayerEvent` enum.

`AdBreakCompletedEventListener`

* **Significado** A reprodução do ad break está concluída.

* **Retorno de chamada para implementar o** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Significado** Um ad break foi ignorado durante a reprodução.

* **Retorno de chamada para implementar o** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Significado** A reprodução do ad break foi iniciada.

* **Retorno de chamada para implementar o** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_START`

`AdClickedEventListener`

* **Significado** Um anúncio foi clicado durante a reprodução.

* **Retorno de chamada para implementar o** `onAdClicked(AdClickEvent event)`
* **Código do evento** `AD_CLICK`

`AdCompletedEventListener`

* **Significado** A reprodução do anúncio está concluída.

* **Retorno de chamada para implementar o** `onAdCompleted(AdPlaybackEvent event)`

* **Código do evento** `AD_COMPLETE`

`AdProgressEventListener`

* **Significado** Relatar o progresso durante a reprodução.

* **Retorno de chamada para implementar o** `onAdProgress(AdPlaybackEvent event)`

* **Código do evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Significado** A resolução de anúncio do Primetime foi concluída. Esse evento só se aplica ao conteúdo de VOD.

* **Retorno de chamada para implementar o** `onAdResolutionComplete()`

* **Código do evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **Significado** A reprodução do anúncio foi iniciada.

* **Retorno de chamada para implementar o** `onAdStarted(AdPlaybackEvent event)`

* **Código do evento** `AD_START`

`AudioUpdatedEventListener`

* **Significado** Foi detectada uma nova faixa de áudio.

* **Retorno de chamada para implementar o** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **Significado** O reprodutor começou a ser armazenado em buffer.

* **Retorno de chamada para implementar o** `onBufferingBegin(BufferEvent event)`

* **Código do evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **Significado** O reprodutor parou de ser armazenado em buffer.

* **Retorno de chamada para implementar o** `onBufferingEnd(BufferEvent event)`

* **Código do evento** `BUFFERING_END`

`BufferPreparedEventListener`

* **Significado** O buffer está preparado.

* **Retorno de chamada para implementar o** `onBufferPrepared()`

* **Código do evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **Significado** Foi detectada uma nova faixa de legenda.

* **Retorno de chamada para implementar o** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **Significado** Um novo metadado de DRM foi detectado no fluxo de mídia.

* **Retorno de chamada para implementar o** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Código do evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **Significado** Um novo item de reprodutor de mídia foi criado.

* **Retorno de chamada para implementar o** `onItemCreated(MediaPlayerItemEvent event)`

* **Código do evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **Significado** Novas informações de carregamento foram criadas para o item atual.

* **Retorno de chamada para implementar o** `onLoadComplete(MediaPlayerItemEvent event)`

* **Código do evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **Significado** Um novo segmento foi carregado.

* **Retorno de chamada para implementar o** `onLoadInformation(LoadInformationEvent event)`

* **Código do evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Significado** O manifesto ou lista de reprodução principal foi atualizada.

* **Retorno de chamada para implementar o** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **Significado** Falha na operação.

* **Retorno de chamada para implementar o** `onNotification(NotificationEvent event)`

* **Código do evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **Significado** O intervalo de reprodução foi atualizado.

* **Retorno de chamada para implementar o** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Significado** Uma nova taxa de reprodução está visível na tela.

* **Retorno de chamada para implementar o** `onRatePlaying(PlaybackRateEvent event)`

* **Código do evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **Significado** O atributo de taxa do MediaPlayer foi definido.

* **Retorno de chamada para implementar o** `onRateSelected(PlaybackRateEvent event)`

* **Código do evento** `RATE_SELECTED`

`PlayStartEventListener`

* **Significado** A reprodução foi iniciada.

* **Retorno de chamada para implementar o** `onPlayStart()`

* **Código do evento** `PLAY_START`

`ProfileChangeEventListener`

* **Significado** O perfil atual do MediaPlayer foi alterado.

* **Retorno de chamada para implementar o** `onProfileChanged(ProfileEvent event)`

* **Código do evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **Significado** A reprodução atingiu uma reserva de linha do tempo.

* **Retorno de chamada para implementar o** `onReservationReached(ReservationEvent event)`

* **Código do evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Significado** Operação de busca iniciada.

* **Retorno de chamada para implementar o** `onSeekBegin(SeekEvent event)`

* **Código do evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **Significado** A operação de busca foi concluída.

* **Retorno de chamada para implementar o** `onSeekEnd(SeekEvent event)`

* **Código do evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Significado** A posição de busca foi ajustada devido às regras de reprodução internas ou às regras de negócios externas.

* **Retorno de chamada para implementar o** `onPositionAdjusted(SeekEvent event)`

* **Código do evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **Significado** O tamanho da mídia está disponível.

* **Retorno de chamada para implementar o** `onSizeAvailable(SizeAvailableEvent event)`

* **Código do evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **Significado** O estado do MediaPlayer foi alterado.

* **Retorno de chamada para implementar o** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Código do evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **Significado** O indicador de reprodução mudou.

* **Retorno de chamada para implementar o** `onTimeChanged(TimeChangeEvent event)`

* **Código do evento** `TIME_CHANGED`

`TimedEventEventListener`

* **Significado** A operação é concluída com o tempo necessário para a operação.

* **Retorno de chamada para implementar o** `onTimedEvent(TimedEventEvent event)`

* **Código do evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **Significado** Um novo metadado cronometrado foi adicionado a um item em segundo plano.

* **Retorno de chamada para implementar o** `onTimedMetadata(TimedMetadataEvent event)`

* **Código do evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **Significado** Um novo metadado cronometrado foi detectado no fluxo de mídia.

* **Retorno de chamada para implementar o** `onTimedMetadata(TimedMetadataEvent event)`

* **Código do evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **Significado** A linha do tempo foi modificada. Os anúncios podem ter sido adicionados ou removidos da linha do tempo.

* **Retorno de chamada para implementar o** `onTimelineUpdated(TimelineEvent event)`

* **Código do evento** `TIMELINE_UPDATED`
