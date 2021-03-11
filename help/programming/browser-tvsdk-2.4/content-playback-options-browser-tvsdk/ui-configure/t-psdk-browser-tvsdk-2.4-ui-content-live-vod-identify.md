---
description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou VOD.
title: Identifique se o conteúdo é ao vivo ou VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '85'
ht-degree: 0%

---


# Identifique se o conteúdo é ao vivo ou VOD{#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou VOD.

1. Aguarde o TVSDK do navegador acionar um evento `AdobePSDK.PSDKEventType.STATUS_CHANGED` com um `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Essa etapa garante que o recurso de mídia tenha sido carregado com êxito.

   >[!IMPORTANT]
   >
   >Se o TVSDK do navegador não estiver no estado `PREPARED` pelo menos, tentar chamar os seguintes métodos aciona um `IllegalStateException`.

1. Leia `live` da interface `MediaPlayerItem`:

   ```js
   player.currentItem.live
   ```

