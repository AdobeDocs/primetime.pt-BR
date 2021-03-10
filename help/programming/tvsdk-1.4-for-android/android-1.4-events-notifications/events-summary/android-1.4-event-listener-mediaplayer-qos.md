---
description: O TVSDK despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como buffering ou busca.
title: Eventos de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---


# Eventos de QoS{#qos-events}

O TVSDK despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como buffering ou busca.

Para ser notificado sobre todos os eventos relacionados a QoS, registre uma implementação de `MediaPlayer.QOSEventListener` incluindo os seguintes retornos de chamada:

| Evento | Significado |
|---|---|
| [onBufferComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferComplete()) | Buffering concluído. |
| [onBufferStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onBufferStart()) | Buffering iniciado. |
| [onLoadInfo](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onLoadInfo(com.adobe.mediacore.qos.LoadInfo)) (loadInfo) | Um fragmento foi baixado com êxito. |
| [onOperationFailed](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html) (MediaPlayerNotification). [](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) Aviso) | Ocorreu um erro recuperável. |
| [onSeekComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekComplete(long)) (long adaptTime) | A busca foi concluída. |
| [onSeekStart](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.QOSEventListener.html#onSeekStart()) | Busca está começando. |