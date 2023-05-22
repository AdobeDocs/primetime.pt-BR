---
description: Seu aplicativo pode monitorar a atividade no reprodutor e a alteração do status do reprodutor ouvindo os eventos despachados pelo TVSDK.
title: Resumo de eventos do player do Primetime
exl-id: 42489abe-ccaf-4b40-bb4b-de8547b5585a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 0%

---

# Resumo de eventos do player do Primetime {#primetime-player-events-summary-overview}

Seu aplicativo pode monitorar a atividade no reprodutor e a alteração do status do reprodutor ouvindo os eventos despachados pelo TVSDK.

## Eventos {#events}

O TVSDK notifica quando ocorrem eventos aos quais o aplicativo deve responder. Cada evento corresponde a uma classe de ouvinte, com um método de retorno de chamada que você deve implementar.

>[!TIP]
>
>Os códigos de evento são as constantes da variável `MediaPlayerEvent` enum.

## AdBreakCompletedEventListener {#section_D7A74A4EACA44E54806D040491B7D879}

* ** Significado ** A reprodução do ad break está concluída.

* ** Retorno de chamada para implementar ** `onAdBreakCompleted(AdBreakPlaybackEvent event)`

* ** Código do evento ** `AD_BREAK_COMPLETE`

## AdBreakSkippedEventListener {#section_7AE5442442484F45B521D3309691C59C}

* ** Significado ** Um ad break foi ignorado durante a reprodução.

* ** Retorno de chamada para implementar ** `onAdBreakSkipped(AdBreakPlaybackEvent event)`

* ** Código do evento ** `AD_BREAK_SKIPPED`

## AdBreakStartedEventListener {#section_0D50327621164E3A9C8F3337AA20BDE7}

* ** Significado ** A reprodução do ad break foi iniciada.

* ** Retorno de chamada para implementar ** `onAdBreakStarted(AdBreakPlaybackEvent event)`

* ** Código do evento ** `AD_BREAK_START`

## AdClickedEventListener {#section_9A6FD39EEDE0460B94FD074B5C2FB9BE}

* ** Significado ** Um anúncio foi clicado durante a reprodução.

* ** Retorno de chamada para implementar ** `onAdClicked(AdClickEvent event)`

* ** Código do evento ** `AD_CLICK`

## AdCompletedEventListener {#section_D45EA0B1825145259EAC50A3E6B24BFC}

* ** Significado ** A reprodução do anúncio está concluída.

* ** Retorno de chamada para implementar ** `onAdCompleted(AdPlaybackEvent event)`

* ** Código do evento ** `AD_COMPLETE`

## AdProgressEventListener {#section_C26ACC4B941942B0A24DB06585EF52AB}

* ** Ou seja ** Relatar o progresso durante a reprodução.

* ** Retorno de chamada para implementar ** `onAdProgress(AdPlaybackEvent event)`

* ** Código do evento ** `AD_PROGRESS`

## AdResolutionCompleteEventListener {#section_E9D545408CBA448EA2A8606DA629FB0B}

* ** Isso significa que ** o Primetime e a decisão da publicidade estão concluídos. Esse evento só se aplica ao conteúdo de VOD.

* ** Retorno de chamada para implementar ** `onAdResolutionComplete()`

* ** Código do evento ** `AD_RESOLUTION_COMPLETE`

## AdStartedEventListener {#section_A4339C48F82640A8AF4AF09CB3B33188}

* ** Significado ** A reprodução do anúncio foi iniciada.

* ** Retorno de chamada para implementar ** `onAdStarted(AdPlaybackEvent event)`

* ** Código do evento ** `AD_START`

## AudioUpdatedEventListener {#section_06E1A9F683E1411081CFC6BD30C3B669}

* ** Significado ** Foi detectada uma nova faixa de áudio.

* ** Retorno de chamada para implementar ** `onAudioUpdated(MediaPlayerItemEvent event)`

* ** Código do evento ** `AUDIO_TRACK_UPDATED`

## BufferingBeginEventListener {#section_F8378841149A4801867ADDC7C0A98C57}

* ** Significado ** O reprodutor começou a usar buffering.

* ** Retorno de chamada para implementar ** `onBufferingBegin(BufferEvent event)`

* ** Código do evento ** `BUFFERING_BEGIN`

## BufferingEndEventListener {#section_9107E0ED59474F11A04E243C6B117E21}

* ** Significado ** O reprodutor parou de armazenar em buffer.

* ** Retorno de chamada para implementar ** `onBufferingEnd(BufferEvent event)`

* ** Código do evento ** `BUFFERING_END`

## BufferPreparedEventListener {#section_F6BFDF525D8B41B7B6E0EFCCE3065811}

* ** Significado ** O buffer está preparado.

* ** Retorno de chamada para implementar ** `onBufferPrepared()`

* ** Código do evento ** `BUFFER_PREPARED`

## CaptionsUpdatedEventListener {#section_048BB128ADB747519F02DEDDD1C88B86}

* ** Significado ** Uma nova faixa de legenda foi detectada.

* ** Retorno de chamada para implementar ** `onCaptionsUpdated(MediaPlayerItemEvent event)`

* ** Código do evento ** `CAPTIONS_UPDATED`

## DRMMetadataInfoEventListener {#section_CB55064D305A40D5BBAD09A53D63DB95}

* ** Significado ** Um novo metadado de DRM foi detectado no fluxo de mídia.

* ** Retorno de chamada para implementar ** `onDRMMetadataInfo(DRMMetadataInfoEvent event)`

* ** Código do evento ** `DRM_METADATA`

## ItemCreatedEventListener {#section_32A3178664C841008370E8447C978AB2}

* ** Significado ** Um novo item de reprodutor de mídia foi criado.

* ** Retorno de chamada para implementar ** `onItemCreated(MediaPlayerItemEvent event)`

* ** Código do evento ** `ITEM_CREATED`

## ItemLoadCompleteEventListener {#section_E29A3D7D2666461599909BD8E8BA46A7}

* ** Significado ** Novas informações de carga foram criadas para o item atual.

* ** Retorno de chamada para implementar ** `onLoadComplete(MediaPlayerItemEvent event)`

* ** Código do evento ** `ITEM_UPDATED`

## LoadInformationEventListener {#section_A986AD83F68446B99EAC888F98B39148}

* ** Significado ** Um novo segmento foi carregado.

* ** Retorno de chamada para implementar ** `onLoadInformation(LoadInformationEvent event)`

* ** Código do evento ** `LOAD_INFORMATION_AVAILABLE`

## MainManifestUpdatedEventListener {#section_73709D121CED48C1B38550135DA55548}

* ** Significado ** O manifesto ou lista de reprodução principal foi atualizado.

* ** Retorno de chamada para implementar ** `onMainManifestUpdated(MediaPlayerItemEvent event)`

* ** Código do evento ** `MANIFEST_UPDATED`

## NotificationEventListener {#section_E8F27B979D374B5D8EA184E23BC17E43}

* ** Significado ** Falha na operação.

* ** Retorno de chamada para implementar ** `onNotification(NotificationEvent event)`

* ** Código do evento ** `OPERATION_FAILED`

## PlaybackRangeUpdatedEventListener {#section_9072862D7EB842AEA3094DAF911CDF7F}

* ** Significado ** O intervalo de reprodução foi atualizado.

* ** Retorno de chamada para implementar ** `onPlaybackRangeUpdated(MediaPlayerItemEvent event)`

* ** Código do evento ** `PLAYBACK_RANGE_UPDATED`

## TaxaDeReproduçãoReproduzindoOuvinteEvento {#section_548A489ABED44F89BDF29DB9EDD348C5}

* ** Significado ** Uma nova taxa de reprodução é visível na tela.

* ** Retorno de chamada para implementar ** `onRatePlaying(PlaybackRateEvent event)`

* ** Código do evento ** `RATE_PLAYING`

## TaxaDeReproduçãoListenerDeEventosSelecionados {#section_B303BAAFA6D14C1599AD3D7D79D722DD}

* ** Significado ** O atributo de taxa do MediaPlayer foi definido.

* ** Retorno de chamada para implementar ** `onRateSelected(PlaybackRateEvent event)`

* ** Código do evento ** `RATE_SELECTED`

## PlayStartEventListener {#section_1D54CAE387B243679348A26E65B6A3FD}

* ** Significado ** A reprodução começou.

* ** Retorno de chamada para implementar ** `onPlayStart()`

* ** Código do evento ** `PLAY_START`

## ProfileChangeEventListener {#section_EEDF08916D1D40509E64EC180F143C9A}

* ** Significado ** O perfil atual do MediaPlayer foi alterado.

* ** Retorno de chamada para implementar ** `onProfileChanged(ProfileEvent event)`

* ** Código do evento ** `PROFILE_CHANGED`

## ReservationReachedEventListener {#section_31677E931F154E7E86D725B2B046065C}

* ** Significado ** A reprodução atingiu uma reserva de linha do tempo.

* ** Retorno de chamada para implementar ** `onReservationReached(ReservationEvent event)`

* ** Código do evento ** `RESERVATION_REACHED`

## SeekBeginEventListener {#section_749E02ED2B1647438F50224C85260A1D}

* ** Significado ** Operação de busca iniciada.

* ** Retorno de chamada para implementar ** `onSeekBegin(SeekEvent event)`

* ** Código do evento ** `SEEK_BEGIN`

## SeekEndEventListener {#section_4F70BAD695AF4717B2254D9DBA1071E4}

* ** Significado ** A operação de busca foi concluída.

* ** Retorno de chamada para implementar ** `onSeekEnd(SeekEvent event)`

* ** Código do evento ** `SEEK_END`

## BuscarPosiçãoAjustadaOuvinteEvento {#section_01F89B73DBB84BEBBA60D820BF5FAC9A}

* ** Significado ** A posição de busca foi ajustada por causa de regras de reprodução internas ou regras de negócios externas.

* ** Retorno de chamada para implementar ** `onPositionAdjusted(SeekEvent event)`

* ** Código do evento ** `SEEK_POSITION_ADJUSTED`

## SizeAvailableEventListener {#section_90DF6565E59B44B19338A7B89D53BBBF}

* ** Significado ** O tamanho da mídia está disponível.

* ** Retorno de chamada para implementar ** `onSizeAvailable(SizeAvailableEvent event)`

* ** Código do evento ** `SIZE_AVAILABLE`

## StatusChangeEventListener {#section_310D2327089D46358F9CE03EA76F3287}

* ** Significado ** O estado do MediaPlayer foi alterado.

* ** Retorno de chamada para implementar ** `onStatusChanged(MediaPlayerStatusChangeEvent event)`

* ** Código do evento ** `STATUS_CHANGED`

## TimeChangeEventListener {#section_ED3855BD90124D97836B2D0957AD9E0C}

* ** Significado ** O indicador de reprodução mudou.

* ** Retorno de chamada para implementar ** `onTimeChanged(TimeChangeEvent event)`

* ** Código do evento ** `TIME_CHANGED`

## TimedEventEventListener {#section_5E62C2C81C3B4F93B46E7518578456EA}

* ** Significado ** A operação é concluída com o tempo necessário para a operação.

* ** Retorno de chamada para implementar ** `onTimedEvent(TimedEventEvent event)`

* ** Código do evento ** `TIMED_EVENT`

## LinhaDoTempoMetadadosAdicionadosEmSegundoPlanoOuvinteDeEventos {#section_7B923C7116154CCFBAE1FCA92C928EB2}

* ** Significado ** Os novos metadados cronometrados foram adicionados a um item em segundo plano.

* ** Retorno de chamada para implementar ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Código do evento ** `TIMED_METADATA_ADDED_IN_BACKGROUND`

## TimedMetadataEventListener {#section_9741EA321ACF403FB8E9AB311BAACDD7}

* ** Significado ** Um novo metadado cronometrado foi detectado no fluxo de mídia.

* ** Retorno de chamada para implementar ** `onTimedMetadata(TimedMetadataEvent event)`

* ** Código do evento ** `TIMED_METADATA_AVAILABLE`

## TimelineUpdatedEventListener {#section_D0755BD2AF3347C7861395706E31B861}

* ** Significado ** A linha do tempo foi modificada. Os anúncios podem ter sido adicionados ou removidos da linha do tempo.

* ** Retorno de chamada para implementar ** `onTimelineUpdated(TimelineEvent event)`

* ** Código do evento ** `TIMELINE_UPDATED`
