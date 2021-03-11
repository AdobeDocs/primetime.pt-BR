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

1. Certifique-se de que o reprodutor esteja pelo menos no status INICIALIZADO.
1. Determine se o conteúdo `MediaPlayerItem` é ativo (true) ou VOD (false).

   ```
   function get isLive():Boolean;
   ```

