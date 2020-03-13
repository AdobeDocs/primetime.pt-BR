---
description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Selecionar uma faixa de legenda atual entre as faixas disponíveis{#select-a-current-caption-track-from-among-available-tracks}

Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.

>[!TIP]
>
>As legendas ocultas estão sempre ativadas. Todas as faixas de legenda fechada padrão são consideradas como presentes. As faixas padrão (como CC1-CC4, CS1-CS6) são enumeradas em `ClosedCaptionsTrack.DefaultCCTypes`. Quando a reprodução começa, o TVSDK procura atividade em qualquer um desses canais. Se encontrar atividade, ele define o `isActive` método para esse rastreamento e despacha o `MediaPlayer.PlaybackEventListener.onUpdated` evento.

1. Aguarde até que o player de mídia esteja pelo menos no estado PREPARADO.
1. Analise estes eventos:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: A lista inicial de faixas de legenda fechada está disponível

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
seletedClosedCaptionsIndex = i;
}}

```
1. Implement a listener for the event that indicates that more tracks are available. When TVSDK dispatches the event, retrieve the current list of available tracks.

Retrieve the list each time that the event occurs to ensure that you always have the most current list.

