---
description: Você pode selecionar um rastreamento de uma lista de faixas de legendas ocultas disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas faixas podem não estar disponíveis inicialmente, portanto, escute o evento que indica que mais se tornaram disponíveis.
title: Selecionar uma faixa de legenda atual dentre as faixas disponíveis
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 2%

---


# Selecionar uma faixa de legenda atual entre as faixas disponíveis {#select-a-current-caption-track-from-among-available-tracks}

Você pode selecionar um rastreamento de uma lista de faixas de legendas ocultas disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas faixas podem não estar disponíveis inicialmente, portanto, escute o evento que indica que mais se tornaram disponíveis.

1. Aguarde até que o reprodutor de mídia tenha pelo menos o status `PREPARED` .
1. Analise estes eventos:

   * `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.INITIALIZED`: A lista inicial de faixas de legendas ocultas está disponível.

1. Obtenha uma lista de todas as faixas de legendas ocultas atualmente disponíveis.

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

1. Implemente um ouvinte para o evento que indica que mais rastreamentos estão disponíveis. Quando o TVSDK despachar o evento, recupere a lista atual de rastreamentos disponíveis.

   Recupere a lista sempre que o evento ocorrer para garantir que você sempre tenha a lista mais atual.