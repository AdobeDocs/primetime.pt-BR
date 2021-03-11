---
description: Você pode adicionar botões Pausar e Reproduzir para pausar ou reproduzir o vídeo.
title: Reproduzir e pausar um vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo {#play-and-pause-a-video}

Você pode adicionar botões Pausar e Reproduzir para pausar ou reproduzir o vídeo.

1. Para criar um botão de pausa ou reprodução:
   1. Aguarde até que o reprodutor esteja pelo menos no estado preparado.
   1. Para iniciar a reprodução, chame o método `play` :

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar a reprodução, chame o método `pause()` :

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Use o retorno de chamada de evento de status alterado para verificar se há erros ou para tomar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada para `pause()` ou `play()` e transmite informações sobre a alteração de status, incluindo o novo status, como pausado ou reproduzido.