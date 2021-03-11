---
description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
title: Identifique se o conteúdo é ao vivo ou VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---


# Identifique se o conteúdo é ao vivo ou VOD {#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).

1. Certifique-se de que o player esteja no mínimo no estado `PREPARED`.
1. Determine se o conteúdo `MediaPlayerItem` está ativo ( `true`) ou VOD ( `false`).

   ```java
   boolean isLive();
   ```
