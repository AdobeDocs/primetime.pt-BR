---
description: O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.
seo-description: O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.
seo-title: Eventos de reprodução de anúncio
title: Eventos de reprodução de anúncio
uuid: dd6991ae-3e33-4d92-92e9-26b1086a555a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Eventos de reprodução de anúncio{#ad-playback-events}

O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.

Para ser notificado sobre todos os eventos relacionados à reprodução de anúncios, registre uma implementação de `MediaPlayer.AdPlaybackEventListener` incluindo os retornos de chamada a seguir.

>[!TIP]
>
>Quando os anúncios são inseridos ou removidos da mídia, o TVSDK despacha o evento de reprodução [onTimelineUpdates](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significado |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Um intervalo de anúncios foi reproduzido completamente. |
| onAdBreakSkipped | Uma pausa de anúncio foi ignorada durante a reprodução. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Uma pausa de anúncio foi iniciada. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, anúncio, AdClick adClick) | O usuário clicou no anúncio. Fornece informações ao seu aplicativo sobre o anúncio que o usuário clicou, em resposta à chamada do seu aplicativo `notifyClick` no `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, anúncio) | Um anúncio foi reproduzido completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, anúncio, percentual int) | A reprodução do anúncio progrediu. Despachado várias vezes enquanto um anúncio é reproduzido. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, anúncio) | Um anúncio foi iniciado. |