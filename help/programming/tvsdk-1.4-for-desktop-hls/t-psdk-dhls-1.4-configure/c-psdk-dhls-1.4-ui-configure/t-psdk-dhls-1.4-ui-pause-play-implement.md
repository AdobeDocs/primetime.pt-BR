---
description: Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.
seo-description: Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.
seo-title: Reproduzir e pausar um vídeo
title: Reproduzir e pausar um vídeo
uuid: 04b3b23f-5ef1-4cc4-a22f-f6ffa9cefce5
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar comportamento TVSDK para pausar e reproduzir botões.

1. Crie um botão de pausa/reprodução que faça o seguinte.
   1. Aguarde o player ter pelo menos o status PREPARADO.
   1. Para reproduzir o start, chame o método de reprodução TVSDK:

      ```
      function play():void;
      ```

   1. Para pausar a reprodução, chame o método de pausa do TVSDK:

      ```
      function pause():void;
      ```

1. Use o retorno de chamada do evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` para verificar se há erros ou para realizar outras ações apropriadas.

   O TVSDK chama esse retorno de chamada quando o método pause ou play é chamado. O TVSDK transmite informações sobre a alteração de status no retorno de chamada, incluindo o novo status, como PAUSED ou PLAYING.
