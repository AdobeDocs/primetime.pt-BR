---
description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou VOD.
title: Identificar se o conteúdo é em tempo real ou VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---

# Identificar se o conteúdo é em tempo real ou VOD{#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou VOD.

1. Aguarde o TVSDK do navegador acionar um `AdobePSDK.PSDKEventType.STATUS_CHANGED` evento com um `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Essa etapa garante que o recurso de mídia foi carregado com êxito.

   >[!IMPORTANT]
   >
   >Se o TVSDK do navegador não estiver em pelo menos `PREPARED` estado, tentar chamar os seguintes métodos gera um `IllegalStateException`.

1. Ler `live` do `MediaPlayerItem` interface:

   ```js
   player.currentItem.live
   ```
