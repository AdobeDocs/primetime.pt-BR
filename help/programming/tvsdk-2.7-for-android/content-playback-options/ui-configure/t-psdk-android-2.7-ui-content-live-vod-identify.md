---
description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-title: Identifique se o conteúdo é ao vivo ou VOD
title: Identifique se o conteúdo é ao vivo ou VOD
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Identifique se o conteúdo é ao vivo ou VOD {#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).

1. Certifique-se de que o player esteja pelo menos no `PREPARED` estado.
1. Determine se o `MediaPlayerItem` conteúdo é live ( `true`) ou VOD ( `false`).

   ```java
   boolean isLive();
   ```
