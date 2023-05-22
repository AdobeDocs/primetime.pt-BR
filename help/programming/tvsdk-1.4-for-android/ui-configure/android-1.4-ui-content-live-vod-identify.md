---
description: Em alguns casos, é necessário saber se o conteúdo de mídia é em tempo real ou VOD.
title: Identificar se o conteúdo é em tempo real ou VOD
exl-id: b93cc61b-aa72-4edd-a070-93c111dec339
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Identificar se o conteúdo é em tempo real ou VOD{#identify-whether-the-content-is-live-or-vod}

Em alguns casos, é necessário saber se o conteúdo de mídia é em tempo real ou VOD.

1. Certifique-se de que o reprodutor esteja no estado PREPARADO.
1. Determine se o `MediaPlayerItem` O conteúdo é em tempo real (true) ou VOD (false).

   ```java
   boolean isLive();
   ```
