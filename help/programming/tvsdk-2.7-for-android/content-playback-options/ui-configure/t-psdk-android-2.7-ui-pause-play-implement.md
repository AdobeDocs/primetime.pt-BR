---
description: Você pode adicionar botões de pausa e reprodução para pausar ou reproduzir o vídeo.
seo-description: Você pode adicionar botões de pausa e reprodução para pausar ou reproduzir o vídeo.
seo-title: Reproduzir e pausar um vídeo
title: Reproduzir e pausar um vídeo
uuid: 66fefead-7f1d-46ed-a23e-381f25697978
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo {#play-and-pause-a-video}

Você pode adicionar botões de pausa e reprodução para pausar ou reproduzir o vídeo.

1. Para criar um botão de pausa ou reprodução:
   1. Aguarde o jogador estar pelo menos no estado preparado.
   1. Para reproduzir o start, chame o método `play`:

      ```java
      void play() throws MediaPlayerException;
      ```

   1. Para pausar a reprodução, chame o método `pause()`:

      ```java
      void pause() throws MediaPlayerException;
      ```

1. Use o retorno de chamada do evento alterado de status para verificar se há erros ou para realizar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada para `pause()` ou `play()` e transmite informações sobre a alteração de status, incluindo o novo status, como pausado ou reproduzido.

