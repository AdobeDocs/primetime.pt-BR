---
description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-description: Talvez seja necessário saber se o conteúdo de mídia é ao vivo ou vídeo sob demanda (VOD).
seo-title: Identifique se o conteúdo é ao vivo ou VOD
title: Identifique se o conteúdo é ao vivo ou VOD
uuid: e6a66104-97fb-438a-8356-e21f94058c85
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
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
