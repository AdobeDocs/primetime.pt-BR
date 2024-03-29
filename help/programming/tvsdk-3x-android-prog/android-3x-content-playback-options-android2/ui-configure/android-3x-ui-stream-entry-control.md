---
description: Por padrão, ao iniciar a reprodução, a mídia de VOD começa em 0 e a mídia ativa começa no ponto de vida do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.
title: Inserir um fluxo em um horário específico
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# Inserir um fluxo em um horário específico {#enter-a-stream-at-a-specific-time}

Por padrão, ao iniciar a reprodução, a mídia de VOD começa em 0 e a mídia ativa começa no ponto de vida do cliente (MediaPlayer.LIVE_POINT). Você pode substituir o comportamento padrão.

1. Passar uma posição para `MediaPlayer.prepareToPlay`.

   O TVSDK considera que essa posição é o ponto de partida para o ativo e que nenhuma operação de busca é necessária. Se a posição não estiver dentro do intervalo pesquisável, o TVSDK usará a posição padrão. Para obter mais informações, consulte [Carregar um recurso de mídia no reprodutor de mídia](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

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
