---
description: Você pode adicionar o comportamento TVSDK do navegador para pausar e reproduzir botões.
title: Reproduzir e pausar um vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---

# Reproduzir e pausar um vídeo{#play-and-pause-a-video}

Você pode adicionar o comportamento TVSDK do navegador para pausar e reproduzir botões.

1. Crie um botão Pausar/Reproduzir que faça o seguinte.
   1. Aguarde até que o reprodutor esteja pelo menos no estado PREPARADO.
   1. Para iniciar a reprodução, chame o método de reprodução TVSDK do navegador:

      ```js
      play() → {AdobePSDK.PSDKErrorCode.SUCCESS}
      ```

   1. Para pausar a reprodução, chame o método de pausa TVSDK do Navegador:

      ```java
      void pause() throws IllegalStateException;
      ```

1. Ouça o `AdobePSDK.MediaPlayerStatusChangeEvent` evento para verificar se há erros ou executar outras ações apropriadas.

   O TVSDK do navegador aciona esse evento quando os métodos de pausa ou reprodução são chamados e transmite informações sobre o objeto de evento, incluindo o novo estado, como `MediaPlayerStatus.PLAYING` ou `MediaPlayerStatus.PAUSED`.
