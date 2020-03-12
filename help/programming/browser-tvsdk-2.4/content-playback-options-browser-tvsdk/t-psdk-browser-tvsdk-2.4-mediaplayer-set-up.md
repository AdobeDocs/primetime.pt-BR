---
description: Um objeto MediaPlayer encapsula o comportamento e a funcionalidade de um player de mídia.
seo-description: Um objeto MediaPlayer encapsula o comportamento e a funcionalidade de um player de mídia.
seo-title: Configurar o MediaPlayer
title: Configurar o MediaPlayer
uuid: 2279e388-6fbc-49a2-8560-218d3d31e1d6
translation-type: tm+mt
source-git-commit: af9b865bc1627a97bf8957b5460ff9b46052a7dc

---


# Configurar o MediaPlayer{#set-up-the-mediaplayer}

Um objeto MediaPlayer encapsula o comportamento e a funcionalidade de um player de mídia.

1. Instancie um `MediaPlayer` usando o seguinte:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Criar uma `MediaPlayerView` instância:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   onde `container` é o `div` elemento de destino que contém seu `HTMLMediaElement`.

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

   Ligue para:

   ```js
   var view = new  
   <codeph>
   AdobePSDK.MediaPlayerView 
   </codeph>( 
         document.getElementById("videoDiv"));  
   ```

1. Anexe sua `MediaPlayerView` instância à sua `MediaPlayer` instância:

   ```js
   player.view = view;
   ```

1. Anexe o elemento de controles personalizados à sua instância do MediaPlayer. `div`

   Por exemplo, em HTML:

   ```
   <div id="videoDiv"> 
      <div id="video-controls"> 
         ..... custom video controls 
      </div> 
   </div>
   ```

   Ligue para:

   ```js
   if (typeof player.getView() !== 'undefined') { 
       var view = player.view; 
       view.attachVideoControls(document.getElementById("video-controls")); 
   }
   ```

A `MediaPlayer` instância agora está disponível e corretamente configurada para exibir o conteúdo de vídeo na tela do dispositivo.
