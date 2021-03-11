---
description: Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.
title: Reproduzir e pausar um vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.

1. Crie um botão pausar/reproduzir que faça o seguinte.
   1. Aguarde até que o reprodutor esteja pelo menos no estado PREPARADO.
   1. Para iniciar a reprodução, chame o método de reprodução TVSDK:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Para pausar a reprodução, chame o método de pausa TVSDK:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Use o retorno de chamada `MediaPlayer.PlaybackEventListener.onStateChanged` para verificar se há erros ou tomar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada quando o método pause ou play é chamado. O TVSDK transmite informações sobre a alteração de estado no retorno de chamada, incluindo o novo estado, como PAUSED ou PLAYING.

