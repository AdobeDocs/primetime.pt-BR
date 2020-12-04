---
description: Por padrão, ao iniciar a reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-description: Por padrão, ao iniciar a reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
seo-title: Insira um fluxo em um horário específico
title: Insira um fluxo em um horário específico
uuid: b315a967-77ad-4352-8a32-f228704d4b20
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 1%

---


# Insira um fluxo em um horário específico {#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, start de mídia VOD em 0 e start de mídia ao vivo no ponto ativo do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

1. Passe uma posição para `MediaPlayer.prepareToPlay`.

   O TVSDK considera a determinada posição como o ponto de partida para o ativo, e nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, o TVSDK usará a posição padrão. Para obter mais informações, consulte [Carregar um recurso de mídia no media player](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

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
