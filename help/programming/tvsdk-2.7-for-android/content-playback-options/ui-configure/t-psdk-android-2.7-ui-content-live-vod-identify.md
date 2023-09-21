---
description: Talvez seja necessário saber se o conteúdo de mídia é em tempo real ou de vídeo sob demanda (VOD).
title: Identificar se o conteúdo é em tempo real ou VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '66'
ht-degree: 0%

---

# Identificar se o conteúdo é em tempo real ou VOD {#identify-whether-the-content-is-live-or-vod}

Talvez seja necessário saber se o conteúdo de mídia é em tempo real ou de vídeo sob demanda (VOD).

1. Certifique-se de que o reprodutor esteja no `PREPARED` estado.
1. Determine se o `MediaPlayerItem` o conteúdo está ativo ( `true`) ou VOD ( `false`).

   ```java
   boolean isLive();
   ```
