---
description: O TVSDK despacha eventos de reprodução de anúncio em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.
title: Eventos de reprodução de anúncio
exl-id: f35e3c6f-1d58-4498-9e3b-cbd53e573ef9
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# Eventos de reprodução de anúncio{#ad-playback-events}

O TVSDK despacha eventos de reprodução de anúncio em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.

Para ser notificado sobre todos os eventos relacionados à reprodução de anúncio, registre uma implementação de `MediaPlayer.AdPlaybackEventListener` incluindo os seguintes retornos de chamada.

>[!TIP]
>
>Quando os anúncios são inseridos ou removidos da mídia, o TVSDK despacha o evento de reprodução [onTimelineUpdated](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated()).

| Evento | Significado |
|---|---|
| [onAdBreakComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Um ad break foi totalmente reproduzido. |
| onAdBreakSkipped | Um ad break foi ignorado durante a reprodução. |
| [onAdBreakStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdBreakStart(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak) | Um ad break foi iniciado. |
| [onAdClick](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdClick(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad,%20com.adobe.mediacore.timeline.advertising.AdClick)) (AdBreak adBreak, Anúncio de anúncio, AdClick adClick) | O usuário clicou no anúncio. Fornece informações ao aplicativo sobre o anúncio em que o usuário clicou, em resposta à chamada do aplicativo `notifyClick` no `MediaPlayerView`. |
| [onAdComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdComplete(com.adobe.mediacore.timeline.advertising.AdBreak)) (AdBreak adBreak, AdBreak) | Um anúncio foi reproduzido completamente. |
| [onAdProgress](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdProgress(com.adobe.mediacore.timeline.advertising.AdBreak,com.adobe.mediacore.timeline.advertising.Ad,%20int)) (AdBreak adBreak, AdBreak, int percentage) | A reprodução do anúncio avançou. Despachado várias vezes enquanto um anúncio é reproduzido. |
| [onAdStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.AdPlaybackEventListener.html#onAdStart(com.adobe.mediacore.timeline.advertising.AdBreak,%20com.adobe.mediacore.timeline.advertising.Ad)) (AdBreak adBreak, AdBreak) | Um anúncio foi iniciado. |
