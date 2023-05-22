---
description: Você pode adicionar o comportamento TVSDK aos botões Pausar e Reproduzir.
title: Reproduzir e pausar um vídeo
exl-id: c1c259a4-edb8-475b-96a2-7fa0903804c3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---

# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar o comportamento TVSDK aos botões Pausar e Reproduzir.

1. Crie um botão Pausar/Reproduzir que faça o seguinte.
   1. Aguarde até que o player tenha pelo menos o status PREPARADO.
   1. Para iniciar a reprodução, chame o método de reprodução TVSDK:

      ```
      function play():void;
      ```

   1. Para pausar a reprodução, chame o método de pausa TVSDK:

      ```
      function pause():void;
      ```

1. Use o retorno de chamada para o `MediaPlayerStatusChangeEvent.STATUS_CHANGED` evento para verificar se há erros ou executar outras ações apropriadas.

   O TVSDK chama essa chamada de retorno quando o método pause ou play é chamado. O TVSDK transmite informações sobre a alteração de status na chamada de retorno, incluindo o novo status, como PAUSADO ou REPRODUZINDO.
