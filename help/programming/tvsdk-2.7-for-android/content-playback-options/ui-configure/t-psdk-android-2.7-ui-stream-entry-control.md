---
description: Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 e a mídia ao vivo é iniciada no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-description: Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 e a mídia ao vivo é iniciada no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-title: Insira um fluxo em um horário específico
title: Insira um fluxo em um horário específico
uuid: 65a19192-b890-4d69-9cb1-582a22988d2b
translation-type: tm+mt
source-git-commit: fd686391df0fa711bba99bc1bc312c9ef619f184

---


# Insira um fluxo em um horário específico {#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, a mídia VOD é iniciada em 0 e a mídia ao vivo é iniciada no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

1. Passe uma posição para `MediaPlayer.prepareToPlay`.

   O TVSDK considera a determinada posição como o ponto de partida para o ativo, e nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, o TVSDK usará a posição padrão. Para obter mais informações, consulte [Carregar um recurso de mídia no player](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md)de mídia.

   Por exemplo:

   ```java
   long desiredPostion = // TODO : choose a value; 
   @Override 
   public void onStatusChanged(MediaPlayerStatusChangedEvent statusChangedEvent) {   
       switch (statusChangedEvent.getStatus()) { 
           case INITIALIZED: 
               _mediaPlayer.prepareToPlay(desiredPosition); 
               break; 
           case PREPARING: 
               showBufferingSpinner(); 
               break; 
       } 
   }
   ```

