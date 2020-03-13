---
description: Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.
seo-description: Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.
seo-title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
uuid: ee2bda5e-e398-4d09-bc5c-5a6adbf5f603
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Selecionar uma faixa de legenda atual entre as faixas disponíveis {#select-a-current-caption-track-from-among-available-tracks}

Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.

1. Aguarde até que o player de mídia tenha pelo menos o `PREPARED` status.
1. Analise estes eventos:

   * `MediaPlayerEvent.STATUS_CHANGED` com status `MediaPlayerStatus.INITIALIZED`: A lista inicial de faixas de legenda fechada está disponível.

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

1. Implemente um ouvinte para o evento que indica que há mais faixas disponíveis. Quando o TVSDK despachar o evento, recupere a lista atual de rastreamentos disponíveis.

   Recupere a lista sempre que o evento ocorrer para garantir que você sempre tenha a lista mais atual.