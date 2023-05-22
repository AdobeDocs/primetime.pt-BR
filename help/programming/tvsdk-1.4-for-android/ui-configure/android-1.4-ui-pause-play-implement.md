---
description: Você pode adicionar o comportamento TVSDK aos botões Pausar e Reproduzir.
title: Reproduzir e pausar um vídeo
exl-id: 62e77f50-5133-4db5-bf10-fde7d28e959d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar o comportamento TVSDK aos botões Pausar e Reproduzir.

1. Crie um botão Pausar/Reproduzir que faça o seguinte.
   1. Aguarde até que o reprodutor esteja pelo menos no estado PREPARADO.
   1. Para iniciar a reprodução, chame o método de reprodução TVSDK:

      ```java
      void play() throws IllegalStateException;
      ```

   1. Para pausar a reprodução, chame o método de pausa TVSDK:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Use o `MediaPlayer.PlaybackEventListener.onStateChanged` retorno de chamada para verificar se há erros ou executar outras ações apropriadas.

   O TVSDK chama essa chamada de retorno quando o método pause ou play é chamado. O TVSDK transmite informações sobre a alteração de estado na chamada de retorno, incluindo o novo estado, como PAUSADO ou REPRODUZINDO.
