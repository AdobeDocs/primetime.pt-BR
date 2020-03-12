---
description: Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, acompanhando os eventos despachados pelo TVSDK.
seo-description: Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, acompanhando os eventos despachados pelo TVSDK.
seo-title: Resumo dos eventos do player Primetime
title: Resumo dos eventos do player Primetime
uuid: b2ff74f2-c373-42da-a717-2f0550cbcb7f
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Resumo dos eventos do player Primetime {#primetime-player-events-summary}

Seu aplicativo pode monitorar a atividade no player e a alteração do status do player, acompanhando os eventos despachados pelo TVSDK.

## Eventos {#events}

O TVSDK notifica quando ocorrem eventos, aos quais seu aplicativo deve responder. Cada evento corresponde a uma classe de ouvinte, com um método de retorno de chamada que você deve implementar.

>[!TIP]
>
>Os códigos de evento são as constantes da `MediaPlayerEvent` enumeração.

`AdBreakCompletedEventListener`

* **Ou seja** , a reprodução do intervalo do anúncio está concluída.

* **Retorno de chamada para implementar**`onAdBreakCompleted(AdBreakPlaybackEvent event)`

* **Código** do evento `AD_BREAK_COMPLETE`

`AdBreakSkippedEventListener`

* **Ou seja** , uma pausa de anúncio foi ignorada durante a reprodução.

* **Retorno de chamada para implementar**`onAdBreakSkipped(AdBreakPlaybackEvent event)`

* **Código** do evento `AD_BREAK_SKIPPED`

`AdBreakStartedEventListener`

* **Ou seja** , a reprodução do intervalo do anúncio foi iniciada.

* **Retorno de chamada para implementar**`onAdBreakStarted(AdBreakPlaybackEvent event)`

* **Código** do evento `AD_BREAK_START`

`AdClickedEventListener`

* **Ou seja** , um anúncio foi clicado durante a reprodução.

* **Retorno de chamada para implementar**`onAdClicked(AdClickEvent event)`
* **Código** do evento `AD_CLICK`

`AdCompletedEventListener`

* **Ou seja** , a reprodução do anúncio está concluída.

* **Retorno de chamada para implementar**`onAdCompleted(AdPlaybackEvent event)`

* **Código** do evento `AD_COMPLETE`

`AdProgressEventListener`

* **Significado** do andamento dos relatórios durante a reprodução.

* **Retorno de chamada para implementar**`onAdProgress(AdPlaybackEvent event)`

* **Código** do evento `AD_PROGRESS`

`AdResolutionCompleteEventListener`

* **Ou seja** , a decisão do anúncio Primetime está concluída. Esse evento só se aplica ao conteúdo VOD.

* **Retorno de chamada para implementar**`onAdResolutionComplete()`

* **Código** do evento `AD_RESOLUTION_COMPLETE`

`AdStartedEventListener`{#section_A4339C48F82640A8AF4AF09CB3B33188}

* **Ou seja** , a reprodução do anúncio começou.

* **Retorno de chamada para implementar**`onAdStarted(AdPlaybackEvent event)`

* **Código** do evento `AD_START`

`AudioUpdatedEventListener`

* **Significando** que uma nova faixa de áudio foi detectada.

* **Retorno de chamada para implementar**`onAudioUpdated(MediaPlayerItemEvent event)`

* **Código** do evento `AUDIO_TRACK_UPDATED`

`BufferingBeginEventListener`

* **Ou seja** , o player iniciou o buffering.

* **Retorno de chamada para implementar**`onBufferingBegin(BufferEvent event)`

* **Código** do evento `BUFFERING_BEGIN`

`BufferingEndEventListener`

* **Ou seja** , o player interrompeu o buffering.

* **Retorno de chamada para implementar**`onBufferingEnd(BufferEvent event)`

* **Código** do evento `BUFFERING_END`

`BufferPreachedEventListener&#39;

* **Ou seja** , o buffer está preparado.

* **Retorno de chamada para implementar**`onBufferPrepared()`

* **Código** do evento `BUFFER_PREPARED`

`CaptionsUpdatedEventListener`

* **Significando** que um novo rastreamento de legenda foi detectado.

* **Retorno de chamada para implementar**`onCaptionsUpdated(MediaPlayerItemEvent event)`

* **Código** do evento `CAPTIONS_UPDATED`

`DRMMetadataInfoEventListener`

* **Ou seja** , foram detectados novos metadados DRM no fluxo de mídia.

* **Retorno de chamada para implementar**`onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* **Código** do evento `DRM_METADATA`

`ItemCreatedEventListener`

* **Ou seja** , um novo item de player de mídia foi criado.

* **Retorno de chamada para implementar**`onItemCreated(MediaPlayerItemEvent event)`

* **Código** do evento `ITEM_CREATED`

`ItemLoadCompleteEventListener`

* **Significando** que novas informações de carregamento foram criadas para o item atual.

* **Retorno de chamada para implementar**`onLoadComplete(MediaPlayerItemEvent event)`

* **Código** do evento `ITEM_UPDATED`

`LoadInformationEventListener`

* **Significando** que um novo segmento foi carregado.

* **Retorno de chamada para implementar**`onLoadInformation(LoadInformationEvent event)`

* **Código** do evento `LOAD_INFORMATION_AVAILABLE`

`MainManifestUpdatedEventListener`

* **Ou seja** , o manifesto ou a lista de reprodução principal foi atualizada.

* **Retorno de chamada para implementar**`onMainManifestUpdated(MediaPlayerItemEvent event)`

* **Código** do evento `MANIFEST_UPDATED`

`NotificationEventListener`

* **Ou seja** , a operação falhou.

* **Retorno de chamada para implementar**`onNotification(NotificationEvent event)`

* **Código** do evento `OPERATION_FAILED`

`PlaybackRangeUpdatedEventListener`

* **Significando** que o intervalo de reprodução foi atualizado.

* **Retorno de chamada para implementar**`onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* **Código** do evento `PLAYBACK_RANGE_UPDATED`

`PlaybackRatePlayingEventListener`

* **Ou seja** , uma nova taxa de reprodução está visível na tela.

* **Retorno de chamada para implementar**`onRatePlaying(PlaybackRateEvent event)`

* **Código** do evento `RATE_PLAYING`

`PlaybackRateSelectedEventListener`

* **Ou seja** , o atributo de taxa do MediaPlayer foi definido.

* **Retorno de chamada para implementar**`onRateSelected(PlaybackRateEvent event)`

* **Código** do evento `RATE_SELECTED`

`PlayStartEventListener`

* **Ou seja** , a reprodução foi iniciada.

* **Retorno de chamada para implementar**`onPlayStart()`

* **Código** do evento `PLAY_START`

`ProfileChangeEventListener`

* **Ou seja** , o perfil atual do MediaPlayer foi alterado.

* **Retorno de chamada para implementar**`onProfileChanged(ProfileEvent event)`

* **Código** do evento `PROFILE_CHANGED`

`ReservationReachedEventListener`

* **Ou seja** , a reprodução atingiu uma reserva de linha do tempo.

* **Retorno de chamada para implementar**`onReservationReached(ReservationEvent event)`

* **Código** do evento `RESERVATION_REACHED`

`SeekBeginEventListener`

* **Ou seja** , a operação de busca foi iniciada.

* **Retorno de chamada para implementar**`onSeekBegin(SeekEvent event)`

* **Código** do evento `SEEK_BEGIN`

`SeekEndEventListener`

* **Ou seja** , a operação de busca foi concluída.

* **Retorno de chamada para implementar**`onSeekEnd(SeekEvent event)`

* **Código** do evento `SEEK_END`

`SeekPositionAdjustedEventListener`

* **Ou seja** , a posição de busca foi ajustada devido às regras de reprodução interna ou às regras comerciais externas.

* **Retorno de chamada para implementar**`onPositionAdjusted(SeekEvent event)`

* **Código** do evento `SEEK_POSITION_ADJUSTED`

`SizeAvailableEventListener`

* **Significado** O tamanho da mídia está disponível.

* **Retorno de chamada para implementar**`onSizeAvailable(SizeAvailableEvent event)`

* **Código** do evento `SIZE_AVAILABLE`

`StatusChangeEventListener`

* **Ou seja** , o estado do MediaPlayer foi alterado.

* **Retorno de chamada para implementar**`onStatusChanged(MediaPlayerStatusChangeEvent event)`

* **Código** do evento `STATUS_CHANGED`

`TimeChangeEventListener`

* **Significando** que o indicador de reprodução mudou.

* **Retorno de chamada para implementar**`onTimeChanged(TimeChangeEvent event)`

* **Código** do evento `TIME_CHANGED`

`TimedEventEventListener`

* **Ou seja** , a operação está concluída com o tempo necessário para a operação.

* **Retorno de chamada para implementar**`onTimedEvent(TimedEventEvent event)`

* **Código** do evento `TIMED_EVENT`

`TimelineMetadataAddedInBackgroundEventListener`

* **Ou seja** , novos metadados cronometrados foram adicionados a um item em segundo plano.

* **Retorno de chamada para implementar**`onTimedMetadata(TimedMetadataEvent event)`

* **Código** do evento `TIMED_METADATA_ADDED_IN_BACKGROUND`

`TimedMetadataEventListener`

* **Ou seja** , novos metadados cronometrados foram detectados no fluxo de mídia.

* **Retorno de chamada para implementar**`onTimedMetadata(TimedMetadataEvent event)`

* **Código** do evento `TIMED_METADATA_AVAILABLE`

`TimelineUpdatedEventListener`

* **Significado** A linha do tempo foi modificada. Os anúncios podem ter sido adicionados ou removidos da linha do tempo.

* **Retorno de chamada para implementar**`onTimelineUpdated(TimelineEvent event)`

* **Código** do evento `TIMELINE_UPDATED`