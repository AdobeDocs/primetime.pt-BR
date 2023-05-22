---
description: Conclua as etapas a seguir para criar um reprodutor básico usando o TVSDK do navegador.
title: Criar um reprodutor básico usando o TVSDK
exl-id: ea7485e0-5d15-469b-b8b6-f9604d283492
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Criar um reprodutor básico usando o TVSDK{#create-a-basic-player-using-tvsdk}

Conclua as etapas a seguir para criar um reprodutor básico usando o TVSDK do navegador.

1. Crie um novo diretório no qual você possa baixar os arquivos compactados para o TVSDK do navegador.
1. Baixe o navegador TVSDK do Zendesk, descompacte os arquivos e coloque a pasta de estruturas no novo diretório.
1. Crie uma placa de formatação de HTML simples para o código com uma `div` nele.
1. Coloque esse modelo em um arquivo HTML no diretório criado na etapa 1.

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

1. Para a tag body, adicione o `onLoad` seção.

   ```
   <body onload="startVideo()">
   ```

1. Comece a implementar o `startVideo` função.
1. Adicione uma tag de script e crie o `startVideo` na tag.

   Isso deve estar na seção de cabeçalho da página.

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
   >É aqui que a `div` que você criou anteriormente será usado.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Adicione o ouvinte de eventos do player.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente o manipulador de eventos e coloque-o antes do ouvinte de eventos de adição.

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

1. Crie o `MediaResource`, que passa o link M3U8 (ou mpd).

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

1. Quando o reprodutor estiver no estado INICIALIZADO, chame `prepareToPlay`.

   ```js
   case INITIALIZED: 
    player.prepareToPlay(); // <- add this line 
    break;
   ```

1. Depois que o reprodutor estiver no estado PREPARADO, chame `play`.

   ```js
   case PREPARED: 
    player.play(); 
    break;
   ```
