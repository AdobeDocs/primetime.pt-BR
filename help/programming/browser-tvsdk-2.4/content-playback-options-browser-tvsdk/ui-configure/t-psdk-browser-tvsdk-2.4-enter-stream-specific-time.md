---
description: Por padrão, quando a reprodução é iniciada, a mídia de VOD é iniciada em 0 e a mídia ativa é iniciada no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
title: Inserir um fluxo em um horário específico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 0%

---

# Inserir um fluxo em um horário específico{#enter-a-stream-at-a-specific-time}

Por padrão, quando a reprodução é iniciada, a mídia de VOD é iniciada em 0 e a mídia ativa é iniciada no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

1. Passar uma posição para `MediaPlayer.prepareToPlay`.
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
