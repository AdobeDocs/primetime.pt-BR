---
description: A interface MediaPlayer para Android encapsula a funcionalidade e o comportamento de um reprodutor de mídia.
title: Configurar o MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---


# Configurar o MediaPlayer {#set-up-the-mediaplayer}

A interface MediaPlayer para Android encapsula a funcionalidade e o comportamento de um reprodutor de mídia.

O TVSDK fornece uma implementação da interface `MediaPlayer`, a classe `DefaultMediaPlayer`. Quando precisar da funcionalidade de reprodução de vídeo, exemplifique `DefaultMediaPlayer`.

>[!TIP]
>
>Interaja com a instância `DefaultMediaPlayer` somente com os métodos que são expostos pela interface `MediaPlayer`.

1. Instancie um MediaPlayer usando o método de fábrica `DefaultMediaPlayer.create` público, transmitindo um objeto de contexto de aplicativo Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Chame `MediaPlayer.getView` para obter uma referência para a instância `MediaPlayerView`.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Coloque a instância `MediaPlayerView` em uma instância `FrameLayout`, que coloca o vídeo na tela do dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

A instância `MediaPlayer` agora está disponível e corretamente configurada para exibir o conteúdo de vídeo na tela do dispositivo.
