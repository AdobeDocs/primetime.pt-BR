---
description: Você pode adicionar o comportamento TVSDK do navegador para pausar e reproduzir botões.
seo-description: Você pode adicionar o comportamento TVSDK do navegador para pausar e reproduzir botões.
seo-title: Reproduzir e pausar um vídeo
title: Reproduzir e pausar um vídeo
uuid: 4053ea9e-6b74-41e9-ad04-087ad13e3698
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar o comportamento TVSDK do navegador para pausar e reproduzir botões.

1. Crie um botão de pausa/reprodução que faça o seguinte.
   1. Aguarde o player estar no estado PREPARADO.
   1. Para reproduzir o start, chame o método de reprodução TVSDK do navegador:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Para pausar a reprodução, chame o método de pausa TVSDK do navegador:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Analise o evento `AdobePSDK.MediaPlayerStatusChangeEvent` para verificar se há erros ou para tomar outras ações apropriadas.

   O TVSDK do navegador aciona esse evento quando os métodos de pausa ou reprodução são chamados e transmite informações sobre o objeto do evento, incluindo o novo estado, como `MediaPlayerStatus.PLAYING` ou `MediaPlayerStatus.PAUSED`.

