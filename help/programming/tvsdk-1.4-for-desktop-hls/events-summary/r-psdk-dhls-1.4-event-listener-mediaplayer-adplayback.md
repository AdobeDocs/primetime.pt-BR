---
description: O TVSDK despacha eventos de reprodução de anúncio em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.
title: Eventos de reprodução de anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Eventos de reprodução de anúncio {#ad-playback-events}

O TVSDK despacha eventos de reprodução de anúncio em resposta a operações relacionadas a anúncios, como quando um anúncio começa a ser reproduzido.

Para ser notificado sobre todos os eventos relacionados à reprodução de anúncio, registre os ouvintes com o `MediaPlayer` para os eventos a seguir.

>[!TIP]
>
>Quando os anúncios são inseridos ou removidos da mídia, o TVSDK despacha o evento de reprodução TimelineEvent.[LINHA DO TEMPO_ATUALIZADA](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED).

| Evento | Significado |
|---|---|
| AdBreakPlaybackEvent.[AD_BREAK_COMPLETED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_COMPLETED) | Um ad break foi totalmente reproduzido. |
| AdBreakPlaybackEvent.[AD_BREAK_SKIPPED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_SKIPPED) | Um ad break foi ignorado durante a reprodução. |
| AdBreakPlaybackEvent.[AD_BREAK_STARTED](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdBreakPlaybackEvent.html#AD_BREAK_STARTED) | Um ad break foi iniciado. |
| AdClickEvent.[AD_CLICK](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdClickEvent.html#AD_CLICK) | O usuário clicou no anúncio. Fornece informações ao aplicativo sobre o anúncio em que o usuário clicou, em resposta à chamada do aplicativo `notifyClick` no `MediaPlayerView`. |
| AdPlaybackEvent.[ANÚNCIO _CONCLUÍDO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_COMPLETED) | Um anúncio foi reproduzido completamente. |
| AdPlaybackEvent.[_PROGRESSO DO ANÚNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_PROGRESS) | A reprodução do anúncio avançou. Despachado várias vezes enquanto um anúncio é reproduzido. |
| AdPlaybackEvent.[_BUSCA DE ANÚNCIO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Ocorreu uma busca além dos limites do anúncio ou em um anúncio. |
| AdPlaybackEvent.[ANÚNCIO _INICIADO](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/AdPlaybackEvent.html#AD_STARTED) | Um anúncio foi iniciado. |
