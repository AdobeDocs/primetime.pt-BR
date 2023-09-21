---
description: O TVSDK despacha eventos de itens de reprodutor de mídia em resposta ao carregamento de um item de mídia.
title: Eventos carregadores
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 0%

---

# Eventos carregadores{#loader-events}

O TVSDK despacha eventos de itens de reprodutor de mídia em resposta ao carregamento de um item de mídia.

Esses eventos fornecem um fluxo de trabalho alternativo. Não é necessário implementar essa interface ao criar um MediaPlayer. Use isso quando quiser ter um `MediaPlayerItemLoader`.

Para ser notificado sobre eventos relacionados ao carregamento de um recurso de reprodutor de mídia, registre uma implementação de `MediaPlayerItemLoader.LoaderListener` incluindo os eventos a seguir.

| Evento | Significado |
|---|---|
| [onLoadComplete](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onLoadComplete(com.adobe.mediacore.MediaPlayerItem))([mediaPlayerItem](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItem.html) playerItem) | O carregamento do recurso de mídia foi concluído com êxito. |
| [onError](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerItemLoader.LoaderListener.html#onError(com.adobe.ave.MediaErrorCode,%20java.lang.String)) | Ocorreu um problema com o carregamento do recurso de mídia. |

>[!NOTE]
>
>Consulte também `onLoadInfo (loadInfo)` em Eventos de QoS.
