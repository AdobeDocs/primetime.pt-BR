---
description: O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.
title: Eventos de reprodução do anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---


# Eventos de reprodução de anúncio {#ad-playback-events}

O TVSDK despacha eventos de reprodução de anúncios em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.

Para ser notificado sobre todos os eventos relacionados à reprodução de anúncios, registre os ouvintes com o objeto `MediaPlayer` para os seguintes eventos.

>[!TIP]
>
>Quando anúncios são inseridos ou removidos da mídia, o TVSDK despacha o evento de reprodução TimelineEvent.[TIMELINE_UPDATED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significado |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Um ad break foi reproduzido completamente. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Um ad break foi ignorado durante a reprodução. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | Um ad break foi iniciado. |
| AdClickEvent.[_CLIQUE NO ANÚNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | O usuário clicou no anúncio. Fornece informações ao seu aplicativo sobre o anúncio que o usuário clicou, em resposta ao seu aplicativo chamar `notifyClick` no `MediaPlayerView`. |
| AdPlaybackEvent.[_CONCLUÍDO DO ANÚNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Um anúncio foi reproduzido completamente. |
| AdPlaybackEvent.[_PROGRESSO DA PUBLICIDADE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | A reprodução do anúncio progrediu. Despachado várias vezes enquanto um anúncio é reproduzido. |
| AdPlaybackEvent.[_BUSCA DE ANÚNCIOS](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Uma busca ocorreu dentro dos limites do anúncio ou dentro de um anúncio. |
| AdPlaybackEvent.[_INÍCIO DA PUBLICIDADE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Um anúncio foi iniciado. |