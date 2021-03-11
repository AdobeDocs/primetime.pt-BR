---
description: Por padrão, ao iniciar a reprodução, a mídia de VOD é iniciada em 0 (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
title: Insira um fluxo em um horário específico
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 2%

---


# Insira um fluxo em um horário específico {#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, a mídia de VOD é iniciada em 0 (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

1. Passe uma posição para `MediaPlayer.prepareToPlay`.

   O TVSDK considera a posição fornecida como o ponto de partida para o ativo. Nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, o TVSDK usará a posição padrão.

   Por exemplo:

   ```java
   long desiredPostion = //TODO : choose a value; 
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
               case PREPARING: 
               showBufferingSpinner(); 
               break; 
           ... 
       } 
   } 
   ```

