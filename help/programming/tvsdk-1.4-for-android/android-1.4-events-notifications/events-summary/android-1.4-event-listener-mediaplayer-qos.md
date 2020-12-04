---
description: O TVSDK despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar no cálculo das estatísticas de QoS, como buffering ou busca.
seo-description: O TVSDK despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar no cálculo das estatísticas de QoS, como buffering ou busca.
seo-title: Eventos de QoS
title: Eventos de QoS
uuid: 27f60cd3-d3fc-4ea3-81df-96d0fe9f7068
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Eventos QoS{#qos-events}

O TVSDK despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar no cálculo das estatísticas de QoS, como buffering ou busca.

Para ser notificado sobre todos os eventos relacionados a QoS, registre uma implementação de `MediaPlayer.QOSEventListener` incluindo os seguintes retornos de chamada:

| Evento | Significado |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | Buffering concluído. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Buffering iniciado. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo))(loadInfo) | Um fragmento foi baixado com êxito. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html)(MediaPlayerNotification). [(](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) Aviso) | Ocorreu um erro recuperável. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long))(long adjustmentTime) | A busca está completa. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | Buscar está começando. |