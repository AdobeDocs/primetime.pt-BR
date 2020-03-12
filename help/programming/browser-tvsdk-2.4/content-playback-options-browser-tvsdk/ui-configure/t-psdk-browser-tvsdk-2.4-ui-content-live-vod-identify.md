---
description: Talvez seja necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.
seo-description: Talvez seja necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.
seo-title: Identifique se o conteúdo é ao vivo ou VOD
title: Identifique se o conteúdo é ao vivo ou VOD
uuid: 5455801e-b5eb-4829-bde6-ef4440cd69c5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Identifique se o conteúdo é ao vivo ou VOD{#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.

1. Aguarde o TVSDK do navegador disparar um `AdobePSDK.PSDKEventType.STATUS_CHANGED` evento com um `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

   Esta etapa garante que o recurso de mídia foi carregado com êxito.

   >[!IMPORTANT]
   >
   >Se o TVSDK do navegador não estiver no estado, tentar chamar os métodos a seguir emite um `PREPARED` erro `IllegalStateException`.

1. Leia `live` da `MediaPlayerItem` interface:

   ```js
   player.currentItem.live
   ```

