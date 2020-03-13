---
description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-title: Identifique se o conteúdo é ao vivo ou VOD
title: Identifique se o conteúdo é ao vivo ou VOD
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Identifique se o conteúdo é ao vivo ou VOD {#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).

1. Certifique-se de que o player esteja pelo menos no `PREPARED` estado.
1. Determine se o `MediaPlayerItem` conteúdo é live ( `true`) ou VOD ( `false`).

   ```java
   boolean isLive();
   ```
