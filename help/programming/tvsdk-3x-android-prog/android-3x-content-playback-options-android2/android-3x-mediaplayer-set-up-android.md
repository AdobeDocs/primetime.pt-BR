---
description: O TVSDK fornece ferramentas para a criação de um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime. Ele também fornece vários recursos projetados para maximizar a qualidade da reprodução do vídeo.
seo-description: O TVSDK fornece ferramentas para a criação de um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime. Ele também fornece vários recursos projetados para maximizar a qualidade da reprodução do vídeo.
seo-title: Configurar o Media Player
title: Configurar o Media Player
uuid: 1f672484-b340-4f92-8a47-dad4c9f3b3fc
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Configure o Media Player {#set-up-the-media-player}

O TVSDK fornece ferramentas para a criação de um aplicativo de player de vídeo avançado (seu player do Primetime), que pode ser integrado a outros componentes do Primetime. Ele também fornece vários recursos projetados para maximizar a qualidade da reprodução do vídeo.

<!--<a id="section_1FE83A68DE624F20B52C0959851F5699"></a>-->

Instancie um `MediaPlayer` e insira uma visualização dele em um layout de quadro.

1. Instancie `MediaPlayer`, transmitindo um objeto `android.content.Context` para o construtor:

   ```java
   MediaPlayer mediaPlayer = new MediaPlayer(context);
   ```

1. Forneça um layout de quadro ( `android.widget.FrameLayout`) para manter `ViewGroup` de `mediaPlayer`:

   ```java
   FrameLayout playerFrame = (FrameLayout) _viewGroup.findViewById(R.id.playerFrame);
   ```

   >[!NOTE]
   >
   >Abaixo está o trecho de código para criar `_viewGroup`.

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

   >[!NOTE]
   >
   >A instância `MediaPlayer` ( `mediaPlayer`) agora está disponível e corretamente configurada para exibir o conteúdo de vídeo na tela do dispositivo.