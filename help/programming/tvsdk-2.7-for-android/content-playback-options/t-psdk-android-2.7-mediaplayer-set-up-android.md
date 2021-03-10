---
description: Instancie um MediaPlayer e coloque uma visualização dele em um layout de quadro.
title: Configurar o MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Configurar o MediaPlayer {#set-up-the-mediaplayer}

O TVSDK fornece ferramentas para criar um aplicativo de reprodutor de vídeo avançado (seu reprodutor Primetime), que pode ser integrado a outros componentes do Primetime. Ele também fornece vários recursos projetados para maximizar a qualidade da reprodução do vídeo.

Instancie um MediaPlayer e coloque uma visualização dele em um layout de quadro.

1. Instancie `MediaPlayer`, transmitindo um objeto `android.content.Context` ao construtor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Forneça um layout de quadro ( `android.widget.FrameLayout`) para manter `ViewGroup` de `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   Abaixo está o trecho de código para criar `_viewGroup`.

   ```
   @Override 
    public ViewGroup onCreateView(LayoutInflater inflater, ViewGroup container, 
      Bundle savedInstanceState) { 
     _viewGroup = (ViewGroup) inflater.inflate( 
       R.layout.fragment_player, container, false); 
     return _viewGroup; 
    }
   ```

1. Coloque uma visualização de `mediaPlayer` dentro do layout do quadro:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>A instância `MediaPlayer` ( `mediaPlayer`) agora está disponível e corretamente configurada para exibir o conteúdo de vídeo na tela do dispositivo.