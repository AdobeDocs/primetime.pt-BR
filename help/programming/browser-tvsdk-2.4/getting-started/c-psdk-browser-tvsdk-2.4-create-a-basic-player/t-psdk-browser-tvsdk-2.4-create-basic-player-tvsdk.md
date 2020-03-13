---
description: Complete as etapas a seguir para criar um player básico usando o TVSDK do navegador.
seo-description: Complete as etapas a seguir para criar um player básico usando o TVSDK do navegador.
seo-title: Criar um player básico usando TVSDK
title: Criar um player básico usando TVSDK
uuid: ec15cf53-197f-4190-a6b2-600a57815390
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Criar um player básico usando TVSDK{#create-a-basic-player-using-tvsdk}

Complete as etapas a seguir para criar um player básico usando o TVSDK do navegador.

1. Crie um novo diretório no qual você pode baixar os arquivos compactados para TVSDK do navegador.
1. Baixe o navegador TVSDK do Zendesk, descompacte os arquivos e coloque a pasta frameworks no novo diretório.
1. Crie um padrão estereotipado HTML simples para o código com um `div` nele.
1. Coloque este padrão estereotipado em um arquivo HTML no diretório criado na etapa 1.

   ```
   <!DOCTYPE html> 
   
   <html lang="en"> 
   <head> 
   </head> 
   <body> 
         <div id="videoDiv" width="200" height="200"> 
        <div id="video-controls"></div> 
         </div> 
   </body> 
   </html>
   ```

1. Adicione as bibliotecas TVSDK do navegador na seção head.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. Para a tag body, adicione a `onLoad` seção.

   ```
   <body onload="startVideo()">
   ```

1. Comece a implementar a `startVideo` função.
1. Adicione uma tag de script e crie a `startVideo` função na tag .

   Isso deveria estar na seção de cabeçalho da página.

   ```js
   <script> 
    function startVideo(){ 
    } 
   </script>
   ```

1. Crie o `Adobe.MediaPlayer`.

   ```js
   var player = new AdobePSDK.MediaPlayer();
   ```

1. Crie o `MediaPlayerView`.

   >[!TIP]
   >
   >Este é o local em `div` que você criou anteriormente.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Adicione o ouvinte de eventos do player.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente o manipulador de eventos e coloque-o antes de adicionar o ouvinte de eventos.

   ```js
   var onStatusChange = function (event) { 
    console.log(event.status); 
   
    switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.IDLE: 
      console.log("Player Status: IDLE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
      console.log("Player Status: INITIALIZING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
      console.log("Player Status: INITIALIZED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARING: 
      console.log("Player Status: PREPARING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
      console.log("Player Status: PREPARED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PLAYING: 
      console.log("Player Status: PLAYING"); 
      //update UI play/pause to show pause icon 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.PAUSED: 
      console.log("Player Status: PAUSED"); 
      //update UI play/pause to show play icon & 
      //display pause icon over video 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.SEEKING: 
      console.log("Player Status: SEEKING"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.COMPLETE: 
      console.log("Player Status: COMPLETE"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: RELEASED"); 
      break; 
   
     case AdobePSDK.MediaPlayerStatus.RELEASED: 
      console.log("Player Status: ERROR"); 
      break; 
    } 
   }; 
   ```

1. Crie o `MediaResource`, que passa pelo link M3U8 (ou mpd).

   ```js
   var resourceUrl = "https://example.com/a/yourUrl.m3u8"; 
   var resourceType = AdobePSDK.MediaResourceType.HLS; 
   var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, null, false);
   ```

1. Crie uma configuração vazia e substitua o recurso.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   
   player.replaceCurrentResource(mediaResource, config);
   ```

1. Quando o player estiver no estado INICIALIZADO, ligue `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. Depois que o player estiver no estado PREPARADO, ligue `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```

