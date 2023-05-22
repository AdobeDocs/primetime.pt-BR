---
description: As legendas ocultas exibem a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou o visualizador está com problemas de audição.
title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
exl-id: 75970604-c318-4621-bad3-caab292c8a04
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---

# Selecionar uma faixa de legenda atual entre as faixas disponíveis{#select-a-current-caption-track-from-among-available-tracks}

Você pode selecionar uma faixa em uma lista de faixas de legendas ocultas atualmente disponíveis. Esta se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas faixas podem não estar disponíveis inicialmente, portanto, acompanhe o evento que indica que mais faixas estão disponíveis.

>[!TIP]
>
>As legendas ocultas são sempre ativadas. Todas as faixas de legendas ocultas padrão são consideradas presentes. As faixas padrão (como CC1-CC4, CS1-CS6) são enumeradas em `ClosedCaptionsTrack.DefaultCCTypes`. Quando a reprodução começar, o TVSDK procurará atividade em qualquer um desses canais. Se encontrar atividade, define a variável `isActive` para essa trilha e despacha o `MediaPlayer.PlaybackEventListener.onUpdated` evento.

1. Aguarde até que o reprodutor de mídia esteja no estado PREPARADO.
1. Ouça estes eventos:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: a lista inicial de faixas de legendas ocultas está disponível

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implemente um ouvinte para o evento que indica que mais controles estão disponíveis. Quando o TVSDK despachar o evento, recupere a lista atual de rastreamentos disponíveis.

   Recupere a lista sempre que o evento ocorrer para garantir que você sempre tenha a lista mais atual.
