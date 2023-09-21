---
description: Este é um exemplo de como um usuário pode selecionar uma faixa de legendas ocultas.
title: Permitir que o usuário altere a faixa
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '77'
ht-degree: 0%

---

# Permitir que o usuário altere a faixa{#allow-the-user-to-change-the-track}

Este é um exemplo de como um usuário pode selecionar uma faixa de legendas ocultas.

1. Para exibir as faixas de legendas ocultas disponíveis, use o `MediaPlayerItem.closedCaptionsTracks` propriedade.

   ```js
   var tracks = item.closedCaptionsTracks;
   ```

1. Para definir qual faixa de legenda oculta é a atual, use o `MediaPlayerItem.selectClosedCaptionsTrack` método.
1. Após preparar o item do reprodutor de mídia, recupere-o dele usando o ` MediaPlayer.  currentItem ` método.

   ```js
   // Select the cc track with index k. 
   var item = mediaPlayer.currentItem;     
   var tracks = item.closedCaptionsTracks; 
   
   if (k >= 0 && k < tracks.length) { 
       item.selectClosedCaptionsTrack(tracks[k]); 
   }
   ```
