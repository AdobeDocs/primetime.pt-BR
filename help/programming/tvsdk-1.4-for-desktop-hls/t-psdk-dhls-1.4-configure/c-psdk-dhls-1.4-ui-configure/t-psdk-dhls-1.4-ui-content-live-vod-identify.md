---
description: Em alguns casos, é necessário saber se o conteúdo de mídia é em tempo real ou VOD.
title: Identificar se o conteúdo é em tempo real ou VOD
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identificar se o conteúdo é em tempo real ou VOD{#identify-whether-the-content-is-live-or-vod}

Em alguns casos, é necessário saber se o conteúdo de mídia é em tempo real ou VOD.

1. Verifique se o reprodutor está pelo menos no status INICIALIZADO.
1. Determine se o `MediaPlayerItem` O conteúdo é em tempo real (true) ou VOD (false).

   ```
   function get isLive():Boolean;
   ```
