---
description: Instancie um MediaPlayer e coloque uma exibição dele em um layout de quadro.
title: Configurar o MediaPlayer
exl-id: e8fb6527-154b-4f7e-a128-525b5a3b3474
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Configurar o MediaPlayer {#set-up-the-mediaplayer}

O TVSDK fornece ferramentas para criar um aplicativo de reprodutor de vídeo avançado (seu reprodutor do Primetime), que pode ser integrado a outros componentes do Primetime. Ele também fornece vários recursos projetados para maximizar a qualidade da reprodução de vídeo.

Instancie um MediaPlayer e coloque uma exibição dele em um layout de quadro.

1. Instancie `MediaPlayer`, transmitindo um `android.content.Context` ao construtor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Fornecer um layout de quadro ( `android.widget.FrameLayout`) para manter um `ViewGroup` de `mediaPlayer`:

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

1. Colocar uma exibição de `mediaPlayer` dentro do layout do quadro:

   ```java
   playerFrame.addView(mediaPlayer.getView());
   ```

>A variável `MediaPlayer` instância ( `mediaPlayer`) agora está disponível e corretamente configurado para exibir conteúdo de vídeo na tela do dispositivo.
