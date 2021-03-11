---
description: Por padrão, quando a reprodução é iniciada, a mídia VOD é iniciada em 0 e a mídia ao vivo é iniciada no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
title: Insira um fluxo em um horário específico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# Insira um fluxo em um horário específico{#enter-a-stream-at-a-specific-time}

Por padrão, quando a reprodução é iniciada, a mídia VOD é iniciada em 0 e a mídia ao vivo é iniciada no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

1. Passe uma posição para `MediaPlayer.prepareToPlay`.
1. O TVSDK do navegador usa essa posição como ponto de partida para o ativo.

   >[!NOTE]
   >
   >Nenhuma operação de busca é necessária.

1. Se a posição não estiver dentro do intervalo pesquisável, as posições padrão serão usadas.

   Por exemplo:

   ```js
   var desiredPostion = //choose a value; 
   onStatusChange = function (event) { 
       case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
           console.log("Player Status: INITIALIZED"); 
           player.prepareToPlay(desiredPostion); 
           break; 
   } 
   ```

