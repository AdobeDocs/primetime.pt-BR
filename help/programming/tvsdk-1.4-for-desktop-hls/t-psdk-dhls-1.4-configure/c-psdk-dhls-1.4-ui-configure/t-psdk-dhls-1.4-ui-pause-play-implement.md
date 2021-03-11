---
description: Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.
title: Reproduzir e pausar um vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.

1. Crie um botão pausar/reproduzir que faça o seguinte.
   1. Aguarde até que o reprodutor esteja pelo menos no status PREPARED.
   1. Para iniciar a reprodução, chame o método de reprodução TVSDK:

      ```
      function play():void;
      ```

   1. Para pausar a reprodução, chame o método de pausa TVSDK:

      ```
      function pause():void;
      ```

1. Use o retorno de chamada para o evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` para verificar se há erros ou para tomar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada quando o método pause ou play é chamado. O TVSDK transmite informações sobre a alteração de status no retorno de chamada, incluindo o novo status, como PAUSED ou PLAYING.
