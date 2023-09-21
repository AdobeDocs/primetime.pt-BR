---
description: Você pode adicionar botões Pausar e Reproduzir para pausar ou reproduzir seu vídeo.
title: Reproduzir e pausar um vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Reproduzir e pausar um vídeo {#play-and-pause-a-video}

Você pode adicionar botões Pausar e Reproduzir para pausar ou reproduzir seu vídeo.

1. Para criar um botão Pausar ou Reproduzir:
   1. Aguarde até que o reprodutor esteja pelo menos no estado preparado.
   1. Para iniciar a reprodução, chame o `play` método:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar a reprodução, chame o `pause()` método:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Use o retorno de chamada do evento de alteração de status para verificar se há erros ou executar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada para `pause()` ou `play()` O e o transmitem informações sobre a alteração de status, incluindo o novo status, como pausado ou reproduzindo.
