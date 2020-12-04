---
description: Em alguns casos, é necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.
seo-description: Em alguns casos, é necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.
seo-title: Identifique se o conteúdo é ao vivo ou VOD
title: Identifique se o conteúdo é ao vivo ou VOD
uuid: cd71b8d3-259a-48f8-a6ad-02b57da146a7
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Identifique se o conteúdo é live ou VOD{#identify-whether-the-content-is-live-or-vod}

Em alguns casos, é necessário saber se o conteúdo de mídia é exibido ao vivo ou VOD.

1. Verifique se o player está no estado PREPARADO.
1. Determine se o conteúdo `MediaPlayerItem` é live (true) ou VOD (false).

   ```java
   boolean isLive();
   ```

