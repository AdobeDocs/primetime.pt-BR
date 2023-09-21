---
description: Você pode selecionar uma faixa em uma lista de faixas de legendas ocultas atualmente disponíveis. Esta se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas faixas podem não estar disponíveis inicialmente, portanto, acompanhe o evento que indica que mais faixas estão disponíveis.
title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 0%

---

# Selecionar uma faixa de legenda atual entre as faixas disponíveis {#select-a-current-caption-track-from-among-available-tracks}

Você pode selecionar uma faixa em uma lista de faixas de legendas ocultas atualmente disponíveis. Esta se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas faixas podem não estar disponíveis inicialmente, portanto, acompanhe o evento que indica que mais faixas estão disponíveis.

1. Aguarde o reprodutor de mídia estar no estado `PREPARED` status.
1. Ouça estes eventos:

   * `MediaPlayerEvent.STATUS_CHANGED` com status `MediaPlayerStatus.INITIALIZED`: a lista inicial de faixas de legendas ocultas está disponível.

1. Obtenha uma lista de todas as faixas de legendas ocultas disponíveis no momento.

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

1. Implemente um ouvinte para o evento que indica que mais controles estão disponíveis. Quando o TVSDK despachar o evento, recupere a lista atual de rastreamentos disponíveis.

   Recupere a lista sempre que o evento ocorrer para garantir que você sempre tenha a lista mais atual.
