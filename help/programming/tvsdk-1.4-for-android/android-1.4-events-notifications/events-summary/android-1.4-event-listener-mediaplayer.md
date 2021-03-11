---
description: O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.
title: Eventos de reprodução do anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---


# Eventos de reprodução de anúncio{#ad-playback-events}

O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.

Para ser notificado sobre todos os eventos relacionados à reprodução de anúncios, registre uma implementação de `MediaPlayer.AdPlaybackEventListener` incluindo os retornos de chamada a seguir.

>[!TIP]
>
>Quando anúncios são inseridos ou removidos da mídia, o TVSDK despacha o evento de reprodução [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significado |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak) | Um ad break foi reproduzido completamente. |
| onAdBreakSkipped | Um ad break foi ignorado durante a reprodução. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak) | Um ad break foi iniciado. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick))  (AdBreak adBreak, anúncio, AdClick adClick) | O usuário clicou no anúncio. Fornece informações ao seu aplicativo sobre o anúncio que o usuário clicou, em resposta ao seu aplicativo chamar `notifyClick` no `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak))  (AdBreak adBreak, anúncio) | Um anúncio foi reproduzido completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int))  (AdBreak adBreak, anúncio, int percentual) | A reprodução do anúncio progrediu. Despachado várias vezes enquanto um anúncio é reproduzido. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad))  (AdBreak adBreak, anúncio) | Um anúncio foi iniciado. |