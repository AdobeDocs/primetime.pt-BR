---
description: Este é um exemplo de como um usuário pode selecionar um rastreamento de legenda.
seo-description: Este é um exemplo de como um usuário pode selecionar um rastreamento de legenda.
seo-title: Permitir que o usuário altere a faixa
title: Permitir que o usuário altere a faixa
uuid: bd3d4d20-9b52-4365-b656-83ec2a405a1c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Permitir que o usuário altere a faixa{#allow-the-user-to-change-the-track}

Este é um exemplo de como um usuário pode selecionar um rastreamento de legenda.

1. Para exibir as faixas de legenda fechadas disponíveis, use a `MediaPlayerItem.closedCaptionsTracks` propriedade.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Para definir qual rastreamento de legenda é atual, use o `MediaPlayerItem.selectClosedCaptionsTrack` método.
1. Depois que o item do player de mídia for preparado, recupere-o do player de mídia usando o ` MediaPlayer.  currentItem ` método.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

