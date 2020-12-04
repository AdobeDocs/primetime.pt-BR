---
description: Em alguns casos, é necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.
seo-description: Em alguns casos, é necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.
seo-title: Identifique se o conteúdo é ao vivo ou VOD
title: Identifique se o conteúdo é ao vivo ou VOD
uuid: 4d514c46-a1d0-4721-a423-92108126e37e
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Identifique se o conteúdo é live ou VOD{#identify-whether-the-content-is-live-or-vod}

Em alguns casos, é necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.

1. Certifique-se de que o player tenha pelo menos o status INICIALIZADO.
1. Determine se o conteúdo `MediaPlayerItem` é live (true) ou VOD (false).

   ```
   function get isLive():Boolean;
   ```

