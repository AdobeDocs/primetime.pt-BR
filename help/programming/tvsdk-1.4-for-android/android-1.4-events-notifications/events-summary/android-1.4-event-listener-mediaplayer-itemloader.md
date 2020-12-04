---
description: O TVSDK despacha eventos de item do player de mídia em resposta ao carregamento de um item de mídia.
seo-description: O TVSDK despacha eventos de item do player de mídia em resposta ao carregamento de um item de mídia.
seo-title: Eventos do carregador
title: Eventos do carregador
uuid: 1b401ff5-4313-4c64-8be9-99bdeb58ba2a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Eventos do carregador{#loader-events}

O TVSDK despacha eventos de item do player de mídia em resposta ao carregamento de um item de mídia.

Esses eventos fornecem um fluxo de trabalho alternativo. Não é necessário implementar essa interface ao criar um MediaPlayer. Use-o quando quiser ter um `MediaPlayerItemLoader`.

Para ser notificado sobre eventos relacionados ao carregamento de um recurso de player de mídia, registre uma implementação de `MediaPlayerItemLoader.LoaderListener` incluindo os seguintes eventos.

| Evento | Significado |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) mediaPlayerItemItem) | O carregamento do recurso de mídia foi concluído com êxito. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Ocorreu um problema com o carregamento de recursos de mídia. |

>[!NOTE]
>
>Consulte também `onLoadInfo (loadInfo)` em eventos QoS.

