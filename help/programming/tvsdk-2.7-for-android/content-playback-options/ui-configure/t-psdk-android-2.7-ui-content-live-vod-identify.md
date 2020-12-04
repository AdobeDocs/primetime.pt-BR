---
description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-title: Identifique se o conteúdo é ao vivo ou VOD
title: Identifique se o conteúdo é ao vivo ou VOD
uuid: d49315ee-8cec-4b79-adbd-a49c2a527424
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Identifique se o conteúdo é live ou VOD {#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).

1. Verifique se o player está no estado `PREPARED` pelo menos.
1. Determine se o conteúdo `MediaPlayerItem` está ao vivo ( `true`) ou VOD ( `false`).

   ```java
   boolean isLive();
   ```
