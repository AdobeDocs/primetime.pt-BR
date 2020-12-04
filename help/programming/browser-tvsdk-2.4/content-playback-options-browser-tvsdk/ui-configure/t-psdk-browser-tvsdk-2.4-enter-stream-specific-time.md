---
description: Por padrão, quando start de reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-description: Por padrão, quando start de reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-title: Insira um fluxo em um horário específico
title: Insira um fluxo em um horário específico
uuid: 5db73b50-0629-4fb1-8f12-6c88e4cd7109
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 1%

---


# Insira um fluxo em um horário específico{#enter-a-stream-at-a-specific-time}

Por padrão, quando start de reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

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

