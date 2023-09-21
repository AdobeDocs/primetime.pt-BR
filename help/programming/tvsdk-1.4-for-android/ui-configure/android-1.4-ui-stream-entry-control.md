---
description: Por padrão, ao iniciar a reprodução, a mídia de VOD inicia em 0 (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
title: Inserir um fluxo em um horário específico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '86'
ht-degree: 0%

---

# Inserir um fluxo em um horário específico {#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, a mídia de VOD inicia em 0 (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

1. Passar uma posição para `MediaPlayer.prepareToPlay`.

   O TVSDK considera que essa posição é o ponto de partida para o ativo. Nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, o TVSDK usará a posição padrão.

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
