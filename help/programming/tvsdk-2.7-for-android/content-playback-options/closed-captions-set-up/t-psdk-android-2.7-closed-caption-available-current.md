---
description: Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.
seo-description: Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.
seo-title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
uuid: d582779a-2789-4e2a-85f6-1a0b9b847382
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%

---


# Selecionar uma faixa de legenda atual entre as faixas disponíveis {#select-a-current-caption-track-from-among-available-tracks}

Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.

1. Aguarde até que o player de mídia tenha pelo menos o status `PREPARED`.
1. Analise estes eventos:

   * `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.INITIALIZED`: A lista inicial das faixas de legenda fechada está disponível.

1. Obtenha uma lista de todas as faixas de legenda disponíveis no momento.

   Por exemplo:

   ```java
   List<ClosedCaptionsTrack> ccTracks = 
     mediaPlayer.getCurrentItem().getClosedCaptionsTracks();
   ```

1. Selecione uma faixa disponível para ser a faixa atual.

   Por exemplo:

   ```java
   // Select the initial CC track. 
   for (int i = 0; i < ccTracks.size(); i++) { 
       ClosedCaptionsTrack track = ccTracks.get(i); 
       if (track.getName().equals(INITIAL_CC_TRACK)) { 
       <b>mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track);</b> 
             selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implemente um ouvinte para o evento que indica que há mais trilhas disponíveis. Quando o TVSDK despachar o evento, recupere a lista atual das faixas disponíveis.

   Recupere a lista sempre que o evento ocorrer para garantir que você sempre tenha a lista mais atual.