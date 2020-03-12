---
description: Você pode adicionar botões de pausa e reprodução para pausar ou reproduzir o vídeo.
seo-description: Você pode adicionar botões de pausa e reprodução para pausar ou reproduzir o vídeo.
seo-title: Reproduzir e pausar um vídeo
title: Reproduzir e pausar um vídeo
uuid: 3778a1fb-929c-4579-a14c-561179473dea
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Reproduzir e pausar um vídeo {#play-and-pause-a-video}

Você pode adicionar botões de pausa e reprodução para pausar ou reproduzir o vídeo.

1. Para criar um botão de pausa ou reprodução:
   1. Aguarde o jogador estar pelo menos no estado preparado.
   1. Para iniciar a reprodução, chame o `play` método:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar a reprodução, chame o `pause()` método:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Use o retorno de chamada de evento alterado de status para verificar se há erros ou para realizar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada para `pause()` ou `play()` e transmite informações sobre a alteração de status, incluindo o novo status, como pausado ou reproduzido.