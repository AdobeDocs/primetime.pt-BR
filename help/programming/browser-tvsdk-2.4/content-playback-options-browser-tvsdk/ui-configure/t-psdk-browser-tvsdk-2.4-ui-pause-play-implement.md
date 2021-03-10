---
description: Você pode adicionar comportamento TVSDK do navegador para pausar e reproduzir botões.
title: Reproduzir e pausar um vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar comportamento TVSDK do navegador para pausar e reproduzir botões.

1. Crie um botão pausar/reproduzir que faça o seguinte.
   1. Aguarde até que o reprodutor esteja pelo menos no estado PREPARADO.
   1. Para iniciar a reprodução, chame o método de reprodução TVSDK do navegador:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Para pausar a reprodução, chame o método de pausa TVSDK do navegador:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Analise o evento `AdobePSDK.MediaPlayerStatusChangeEvent` para verificar se há erros ou realizar outras ações apropriadas.

   O TVSDK do navegador aciona esse evento quando métodos de pausa ou reprodução são chamados e transmite informações sobre o objeto do evento, incluindo o novo estado, como `MediaPlayerStatus.PLAYING` ou `MediaPlayerStatus.PAUSED`.

