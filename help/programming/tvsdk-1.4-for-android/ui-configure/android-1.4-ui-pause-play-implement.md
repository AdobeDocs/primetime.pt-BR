---
description: Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.
seo-description: Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.
seo-title: Reproduzir e pausar um vídeo
title: Reproduzir e pausar um vídeo
uuid: 24b26364-5cb8-4a95-9574-cc52ddfa876b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.

1. Crie um botão de pausa/reprodução que faça o seguinte.
   1. Aguarde o player estar no estado PREPARADO.
   1. Para reproduzir o start, chame o método de reprodução TVSDK:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Para pausar a reprodução, chame o método de pausa do TVSDK:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Use o retorno de chamada `MediaPlayer.PlaybackEventListener.onStateChanged` para verificar se há erros ou para realizar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada quando o método pause ou play é chamado. O TVSDK transmite informações sobre a alteração de estado no retorno de chamada, incluindo o novo estado, como PAUSED ou PLAYING.

