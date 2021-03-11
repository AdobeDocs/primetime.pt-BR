---
description: Um objeto MediaPlayer encapsula o comportamento e a funcionalidade de um reprodutor de mídia.
title: Configurar o MediaPlayer
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---


# Configurar o MediaPlayer{#set-up-the-mediaplayer}

Um objeto MediaPlayer encapsula o comportamento e a funcionalidade de um reprodutor de mídia.

1. Instancie um `MediaPlayer` usando o seguinte:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Crie uma instância `MediaPlayerView`:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   onde `container` é o elemento `div` de destino que contém seu `HTMLMediaElement`.

   Por exemplo, em uma página HTML:

   ```
   <div id="videoDiv"> 
   <codeph>
     <div id="video-controls"> 
          ... custom video controls 
     </div> 
   </codeph> 
   </div>
   ```

   Chame:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Anexe sua instância `MediaPlayerView` à instância `MediaPlayer`:

   ```js
   player.view = view;
   ```

1. Anexe o elemento de controles personalizados `div` à instância do MediaPlayer.

   Por exemplo, em HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Chame:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

A instância `MediaPlayer` agora está disponível e corretamente configurada para exibir o conteúdo de vídeo na tela do dispositivo.
