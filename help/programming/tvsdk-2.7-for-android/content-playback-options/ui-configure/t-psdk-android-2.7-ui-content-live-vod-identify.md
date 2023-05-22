---
description: Talvez seja necessário saber se o conteúdo de mídia é em tempo real ou de vídeo sob demanda (VOD).
title: Identificar se o conteúdo é em tempo real ou VOD
exl-id: 756d4f04-d354-4194-80c9-c2ea6198a566
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
