---
description: A interface do MediaPlayer para Android encapsula a funcionalidade e o comportamento de um player de mídia.
seo-description: A interface do MediaPlayer para Android encapsula a funcionalidade e o comportamento de um player de mídia.
seo-title: Configurar o MediaPlayer
title: Configurar o MediaPlayer
uuid: 492b4693-acdf-4213-98e5-d6f0f1ae086d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Configurar o MediaPlayer {#set-up-the-mediaplayer}

A interface do MediaPlayer para Android encapsula a funcionalidade e o comportamento de um player de mídia.

O TVSDK fornece uma implementação da `MediaPlayer` interface, a `DefaultMediaPlayer` classe. Quando precisar da funcionalidade de reprodução de vídeo, instancie `DefaultMediaPlayer`.

>[!TIP]
>
>Interaja com a `DefaultMediaPlayer` instância somente com os métodos expostos pela `MediaPlayer` interface.

1. Instancie um MediaPlayer usando o método de fábrica pública `DefaultMediaPlayer.create` , transmitindo um objeto de contexto de aplicativo Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Chame `MediaPlayer.getView` para obter uma referência para a `MediaPlayerView` instância.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Coloque a `MediaPlayerView` instância em uma `FrameLayout` instância, que coloca o vídeo na tela do dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

A `MediaPlayer` instância agora está disponível e corretamente configurada para exibir o conteúdo de vídeo na tela do dispositivo.
