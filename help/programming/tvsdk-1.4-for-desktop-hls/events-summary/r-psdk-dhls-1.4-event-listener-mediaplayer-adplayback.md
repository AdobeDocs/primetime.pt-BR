---
description: O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um start de anúncio é reproduzido.
seo-description: O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um start de anúncio é reproduzido.
seo-title: Eventos de reprodução de anúncio
title: Eventos de reprodução de anúncio
uuid: 63138237-2315-45ff-914d-369da18fdff7
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Eventos de reprodução de anúncio {#ad-playback-events}

O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um start de anúncio é reproduzido.

Para ser notificado sobre todos os eventos relacionados à reprodução de anúncios, registre os ouvintes com o objeto `MediaPlayer` para os seguintes eventos.

>[!TIP]
>
>Quando os anúncios são inseridos ou removidos da mídia, o TVSDK despacha o evento de reprodução TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significado |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Um intervalo de anúncios foi reproduzido completamente. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Uma pausa de anúncio foi ignorada durante a reprodução. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | Uma pausa de anúncio foi iniciada. |
| AdClickEvent.[_CLIQUE EM ANÚNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | O usuário clicou no anúncio. Fornece informações ao seu aplicativo sobre o anúncio que o usuário clicou, em resposta à chamada do seu aplicativo `notifyClick` no `MediaPlayerView`. |
| AdPlaybackEvent.[AD _CONCLUÍDO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Um anúncio foi reproduzido completamente. |
| AdPlaybackEvent.[_ANÚNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | A reprodução do anúncio progrediu. Despachado várias vezes enquanto um anúncio é reproduzido. |
| AdPlaybackEvent.[ANÚNCIO _SEEK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Ocorreu uma busca entre os limites do anúncio ou dentro de um anúncio. |
| AdPlaybackEvent.[_INÍCIO DO ANÚNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Um anúncio foi iniciado. |