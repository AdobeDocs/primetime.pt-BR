---
description: Instancie um MediaPlayer e insira uma visualização dele em um layout de quadro.
seo-description: Instancie um MediaPlayer e insira uma visualização dele em um layout de quadro.
seo-title: Configurar o MediaPlayer
title: Configurar o MediaPlayer
uuid: 49c3edb9-b6e2-49f8-b4aa-f230af7de6b0
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 0%

---


# Configure o MediaPlayer {#set-up-the-mediaplayer}

O TVSDK fornece ferramentas para a criação de um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime. Ele também fornece vários recursos projetados para maximizar a qualidade da reprodução do vídeo.

Instancie um MediaPlayer e insira uma visualização dele em um layout de quadro.

1. Instancie `MediaPlayer`, transmitindo um objeto `android.content.Context` para o construtor:

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