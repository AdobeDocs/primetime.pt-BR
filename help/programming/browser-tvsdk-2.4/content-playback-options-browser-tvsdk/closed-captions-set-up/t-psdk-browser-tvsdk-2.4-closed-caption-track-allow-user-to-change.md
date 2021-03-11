---
description: Este é um exemplo de como um usuário pode selecionar um rastreamento de legenda.
title: Permitir que o usuário altere a faixa
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---


# Permitir que o usuário altere o rastreamento{#allow-the-user-to-change-the-track}

Este é um exemplo de como um usuário pode selecionar um rastreamento de legenda.

1. Para exibir as faixas de legenda ocultas disponíveis, use a propriedade `MediaPlayerItem.closedCaptionsTracks` .

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Para definir qual rastreamento de legenda fechada está atual, use o método `MediaPlayerItem.selectClosedCaptionsTrack`.
1. Depois que o item do reprodutor de mídia for preparado, recupere-o do reprodutor de mídia usando o método ` MediaPlayer.  currentItem ` .

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```

