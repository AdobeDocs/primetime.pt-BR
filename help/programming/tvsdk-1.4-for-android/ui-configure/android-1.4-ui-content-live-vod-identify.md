---
description: Em alguns casos, é necessário saber se o conteúdo de mídia é ao vivo ou VOD.
title: Identifique se o conteúdo é ao vivo ou VOD
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Identifique se o conteúdo é ao vivo ou VOD{#identify-whether-the-content-is-live-or-vod}

Em alguns casos, é necessário saber se o conteúdo de mídia é ao vivo ou VOD.

1. Certifique-se de que o player esteja no mínimo no estado PREPARADO.
1. Determine se o conteúdo `MediaPlayerItem` é ativo (true) ou VOD (false).

   ```java
   boolean isLive();
   ```

