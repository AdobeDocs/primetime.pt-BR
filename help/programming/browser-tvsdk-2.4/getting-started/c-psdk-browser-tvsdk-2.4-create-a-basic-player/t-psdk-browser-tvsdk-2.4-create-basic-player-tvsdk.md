---
description: Complete as etapas a seguir para criar um reprodutor básico usando o Browser TVSDK.
title: Criar um reprodutor básico usando TVSDK
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Criar um reprodutor básico usando TVSDK{#create-a-basic-player-using-tvsdk}

Complete as etapas a seguir para criar um reprodutor básico usando o Browser TVSDK.

1. Crie um novo diretório no qual você pode baixar os arquivos compactados para Browser TVSDK.
1. Baixe o Browser TVSDK do Zendesk, descompacte os arquivos e coloque a pasta de estruturas no novo diretório.
1. Crie um padrão estereotipado HTML simples para o código com um `div` nele.
1. Coloque este padrão estereotipado em um arquivo HTML no diretório que você criou na etapa 1.

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

1. Adicione as bibliotecas TVSDK do navegador na seção do cabeçalho.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script>
   ```

1. Para a tag body , adicione a seção `onLoad` .

   ```
   <body onload="startVideo()">
   ```

1. Comece a implementar a função `startVideo`.
1. Adicione uma tag de script e crie a função `startVideo` na tag .

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
   >É aqui que o `div` criado anteriormente é usado.

   ```js
   var view = new AdobePSDK.MediaPlayerView( 
   document.getElementById("videoDiv")); 
   player.view = view;
   ```

1. Adicione o ouvinte de evento do player.

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

