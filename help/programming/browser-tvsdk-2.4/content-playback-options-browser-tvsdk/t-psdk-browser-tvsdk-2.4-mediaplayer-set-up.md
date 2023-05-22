---
description: Um objeto MediaPlayer encapsula o comportamento e a funcionalidade de um reprodutor de mídia.
title: Configurar o MediaPlayer
exl-id: f492b2bb-3280-4306-ac4b-8b8d0fd68409
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '91'
ht-degree: 0%

---

# Configurar o MediaPlayer{#set-up-the-mediaplayer}

Um objeto MediaPlayer encapsula o comportamento e a funcionalidade de um reprodutor de mídia.

1. Instanciar um `MediaPlayer` usando o seguinte:

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Criar um `MediaPlayerView` instância:

   ```js
   var view = new AdobePSDK.MediaPlayerView(container);
   ```

   onde `container` é o público alvo `div` elemento que contém seu `HTMLMediaElement`.

   Por exemplo, em uma página de HTML:

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

1. Anexe seu `MediaPlayerView` instância para o seu `MediaPlayer` instância:

   ```js
   player.view = view;
   ```

1. Anexar os controles personalizados `div` elemento à sua ocorrência de MediaPlayer.

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

A variável `MediaPlayer` A instância do agora está disponível e configurada corretamente para exibir conteúdo de vídeo na tela do dispositivo.
