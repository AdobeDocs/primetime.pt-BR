---
description: A interface do MediaPlayer para Android encapsula a funcionalidade e o comportamento de um reprodutor de mídia.
title: Configurar o MediaPlayer
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 0%

---

# Configurar o MediaPlayer {#set-up-the-mediaplayer}

A interface do MediaPlayer para Android encapsula a funcionalidade e o comportamento de um reprodutor de mídia.

O TVSDK fornece uma implementação do `MediaPlayer` , a `DefaultMediaPlayer` classe. Quando precisar da funcionalidade de reprodução de vídeo, exemplifique `DefaultMediaPlayer`.

>[!TIP]
>
>Interaja com o `DefaultMediaPlayer` instância somente com os métodos expostos pela variável `MediaPlayer` interface.

1. Instanciar um MediaPlayer usando o público `DefaultMediaPlayer.create` método de fábrica, transmitindo um objeto de contexto de aplicativo Java Android.

   ```java
   public static MediaPlayer create(Context context) 
   ```

1. Chame `MediaPlayer.getView` para obter uma referência para a variável `MediaPlayerView` instância.

   ```java
   MediaPlayerView getView() throws IllegalStateException; 
   ```

1. Coloque o `MediaPlayerView` instância em um `FrameLayout` que coloca o vídeo na tela do dispositivo.

   ```java
   FrameLayout playerFrame = (FrameLayout) view.findViewById(R.id.playerFrame); 
   playerFrame.addView(mediaPlayer.getView()); 
   ```

A variável `MediaPlayer` A instância do agora está disponível e configurada corretamente para exibir conteúdo de vídeo na tela do dispositivo.
