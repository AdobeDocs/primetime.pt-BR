---
description: Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-description: Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-title: Insira um fluxo em um horário específico
title: Insira um fluxo em um horário específico
uuid: ac3479e2-46a1-4ac8-a9e8-68a23f5dd74d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Insira um fluxo em um horário específico {#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

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

