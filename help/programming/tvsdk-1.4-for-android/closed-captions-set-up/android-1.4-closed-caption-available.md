---
description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-description: A legendagem fechada exibe a parte de áudio de um vídeo como texto na tela quando o som está inaudível ou quando o visualizador está com dificuldade de audição.
seo-title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
title: Selecionar uma faixa de legenda atual entre as faixas disponíveis
uuid: 637a70c9-9bef-4b13-8b1f-62f22f983e80
translation-type: tm+mt
source-git-commit: 53924aa8ba90555d58d15ee10fb14221c7dffaff
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---


# Selecionar uma faixa de legenda atual entre as faixas disponíveis{#select-a-current-caption-track-from-among-available-tracks}

Você pode selecionar uma faixa de uma lista de faixas de legenda disponíveis no momento. Isso se torna a faixa atual, que é exibida quando a visibilidade está ativada. Algumas trilhas podem não estar disponíveis inicialmente, portanto, observe o evento que indica que mais se tornaram disponíveis.

>[!TIP]
>
>As legendas ocultas estão sempre ativadas. Todas as faixas de legenda fechada padrão são consideradas como presentes. As faixas padrão (como CC1-CC4, CS1-CS6) são enumeradas em `ClosedCaptionsTrack.DefaultCCTypes`. Quando a reprodução começa, o TVSDK procura atividade em qualquer um desses canais. Se encontrar atividade, ele define o `isActive` método para esse rastreamento e despacha o `MediaPlayer.PlaybackEventListener.onUpdated` evento.

1. Aguarde até que o player de mídia esteja pelo menos no estado PREPARADO.
1. Analise estes eventos:

   * `MediaPlayer.PlaybackEventListener.onStateChanged with state MediaPlayer.PlayerState.INITIALIZED`: A lista inicial das faixas de legenda fechada está disponível

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
           mediaPlayer.getCurrentItem().selectClosedCaptionsTrack(track); 
           selectedClosedCaptionsIndex = i; 
       } 
   }
   ```

1. Implemente um ouvinte para o evento que indica que há mais trilhas disponíveis. Quando o TVSDK despachar o evento, recupere a lista atual das faixas disponíveis.

   Recupere a lista sempre que o evento ocorrer para garantir que você sempre tenha a lista mais atual.
