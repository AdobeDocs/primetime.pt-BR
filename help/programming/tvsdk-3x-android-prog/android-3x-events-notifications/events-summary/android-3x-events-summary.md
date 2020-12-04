---
description: Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, ouvindo os eventos despachados pelo TVSDK.
seo-description: Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, ouvindo os eventos despachados pelo TVSDK.
seo-title: Resumo dos eventos do player Primetime
title: Resumo dos eventos do player Primetime
uuid: b2ff74f2-c373-42da-a717-2f0550cbcb7f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '598'
ht-degree: 0%

---


# Resumo dos eventos do player Primetime {#primetime-player-events-summary}

Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, ouvindo os eventos despachados pelo TVSDK.

## Eventos {#events}

O TVSDK notifica quando ocorrem eventos, aos quais seu aplicativo deve responder. Cada evento corresponde a uma classe de ouvinte, com um método de retorno de chamada que você deve implementar.

>[!TIP]
>
>Os códigos de evento são as constantes da enumeração `MediaPlayerEvent`.

`AdBreakCompletedEventListener`

* **** SignificadoA reprodução do intervalo do anúncio está concluída.

* **Retorno de chamada para implementar** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **** Significado: uma pausa de anúncio foi ignorada durante a reprodução.

* **Retorno de chamada para implementar** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **** SignificadoA reprodução do intervalo do anúncio foi iniciada.

* **Retorno de chamada para implementar** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Código do evento** `AD_BREAK_START`

`AdClickedEventListener`

* **** Significado: um anúncio foi clicado durante a reprodução.

* **Retorno de chamada para implementar** `onAdClicked(AdClickEvent event)`
* **Código do evento** `AD_CLICK`

`AdCompletedEventListener`

* **** SignificadoA reprodução do anúncio está concluída.

* **Retorno de chamada para implementar** `onAdCompleted(AdPlaybackEvent event)`

* **Código do evento** `AD_COMPLETE`

`AdProgressEventListener`

* **** SignificadoRelatório de progresso durante a reprodução.

* **Retorno de chamada para implementar** `onAdProgress(AdPlaybackEvent event)`

* **Código do evento** `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **** Significado: a resolução do anúncio Primetime está concluída. Este evento só se aplica ao conteúdo VOD.

* **Retorno de chamada para implementar** `onAdResolutionComplete()`

* **Código do evento** `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **** SignificadoA reprodução do anúncio foi iniciada.

* **Retorno de chamada para implementar** `onAdStarted(AdPlaybackEvent event)`

* **Código do evento** `AD_START`

`AudioUpdatedEventListener`

* **** Isso significa que uma nova faixa de áudio foi detectada.

* **Retorno de chamada para implementar** `onAudioUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **** Significado: o player iniciou o buffering.

* **Retorno de chamada para implementar** `onBufferingBegin(BufferEvent event)`

* **Código do evento** `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **** Significado: o player parou de buffering.

* **Retorno de chamada para implementar** `onBufferingEnd(BufferEvent event)`

* **Código do evento** `BUFFERING_END`

`BufferPreachedEventListener&#39;

* **** Isso significa que o buffer está preparado.

* **Retorno de chamada para implementar** `onBufferPrepared()`

* **Código do evento** `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **** SignificadoUm novo rastreamento de legenda foi detectado.

* **Retorno de chamada para implementar** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **** Isso significa que novos metadados DRM foram detectados no fluxo de mídia.

* **Retorno de chamada para implementar** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Código do evento** `DRM_METADATA`

`ItemCreatedEventListener`

* **** SignificadoUm novo item de player de mídia foi criado.

* **Retorno de chamada para implementar** `onItemCreated(MediaPlayerItemEvent event)`

* **Código do evento** `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **** SignificadoNovas informações de carregamento foram criadas para o item atual.

* **Retorno de chamada para implementar** `onLoadComplete(MediaPlayerItemEvent event)`

* **Código do evento** `ITEM_UPDATED`

`LoadInformationEventListener`

* **** SignificadoUm novo segmento foi carregado.

* **Retorno de chamada para implementar** `onLoadInformation(LoadInformationEvent event)`

* **Código do evento** `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **** SignificadoO manifesto ou a lista de reprodução principal foi atualizada.

* **Retorno de chamada para implementar** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `MANIFEST_UPDATED`

`NotificationEventListener`

* **** Significado: a operação falhou.

* **Retorno de chamada para implementar** `onNotification(NotificationEvent event)`

* **Código do evento** `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **** SignificadoO intervalo de reprodução foi atualizado.

* **Retorno de chamada para implementar** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Código do evento** `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **** SignificadoUma nova taxa de reprodução está visível na tela.

* **Retorno de chamada para implementar** `onRatePlaying(PlaybackRateEvent event)`

* **Código do evento** `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **** SignificadoO atributo de taxa do MediaPlayer foi definido.

* **Retorno de chamada para implementar** `onRateSelected(PlaybackRateEvent event)`

* **Código do evento** `RATE_SELECTED`

`PlayStartEventListener`

* **** Isso significa que a reprodução foi iniciada.

* **Retorno de chamada para implementar** `onPlayStart()`

* **Código do evento** `PLAY_START`

`ProfileChangeEventListener`

* **** Significado: o perfil atual do MediaPlayer foi alterado.

* **Retorno de chamada para implementar** `onProfileChanged(ProfileEvent event)`

* **Código do evento** `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **** SignificadoReprodução atingiu uma reserva de linha do tempo.

* **Retorno de chamada para implementar** `onReservationReached(ReservationEvent event)`

* **Código do evento** `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Operação** SignificadoSeek iniciada.

* **Retorno de chamada para implementar** `onSeekBegin(SeekEvent event)`

* **Código do evento** `SEEK_BEGIN`

`SeekEndEventListener`

* **** Significado: a operação de busca foi concluída.

* **Retorno de chamada para implementar** `onSeekEnd(SeekEvent event)`

* **Código do evento** `SEEK_END`

`SeekPositionAdjustedEventListener`

* **** SignificadoA posição de busca foi ajustada devido às regras de reprodução interna ou às regras comerciais externas.

* **Retorno de chamada para implementar** `onPositionAdjusted(SeekEvent event)`

* **Código do evento** `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **** SignificadoO tamanho da mídia está disponível.

* **Retorno de chamada para implementar** `onSizeAvailable(SizeAvailableEvent event)`

* **Código do evento** `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **** Significado: o estado MediaPlayer foi alterado.

* **Retorno de chamada para implementar** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Código do evento** `STATUS_CHANGED`

`TimeChangeEventListener`

* **** Significado: o indicador de reprodução mudou.

* **Retorno de chamada para implementar** `onTimeChanged(TimeChangeEvent event)`

* **Código do evento** `TIME_CHANGED`

`TimedEventEventListener`

* **** SignificadoA operação é concluída com o tempo necessário para a operação.

* **Retorno de chamada para implementar** `onTimedEvent(TimedEventEvent event)`

* **Código do evento** `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **** Isso significa que novos metadados cronometrados foram adicionados a um item em segundo plano.

* **Retorno de chamada para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código do evento** `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **** Isso significa que novos metadados cronometrados foram detectados no fluxo de mídia.

* **Retorno de chamada para implementar** `onTimedMetadata(TimedMetadataEvent event)`

* **Código do evento** `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **** SignificadoA linha do tempo foi modificada. Os anúncios podem ter sido adicionados ou removidos da linha do tempo.

* **Retorno de chamada para implementar** `onTimelineUpdated(TimelineEvent event)`

* **Código do evento** `TIMELINE_UPDATED`