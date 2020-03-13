---
description: nulo
seo-description: nulo
seo-title: Adicionar publicidade
title: Adicionar publicidade
uuid: 7762506f-b55e-445d-b8a2-c1208358a370
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Adicionar publicidade {#add-advertising}

1. Defina os metadados do anúncio.

   ```js
   var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
     auditudeSettings.domain = "auditude.com"; 
     auditudeSettings.mediaId = "adbe_tearsofsteel2"; 
     auditudeSettings.zoneId = "123869";
   ```

1. Adicione os metadados do anúncio ao `MediaResource`.

   ```js
   var mediaResource =  
     new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
   ```

1. Adicione as configurações à configuração e adicione uma fábrica de `SpliceOut` analisadores.

   ```js
   var config = new AdobePSDK.MediaPlayerItemConfig(); 
   config.advertisingMetadata = auditudeSettings; 
   config.advertisingFactory = new ExtCueOutContentFactory(auditudeSettings);
   ```

1. Adicione a seção `ExtCueOutContentFactory` da biblioteca.
1. Baixe a seção `ExtCueOutContentFactory.js` da biblioteca e coloque-a na pasta de trabalho.

   ```js
   <script src= "frameworks/player/dash.min.js"></script> 
   <script src= "frameworks/player/primetimemain.min.js"></script> 
   <script src= "frameworks/player/swfobject.js"></script> 
   <script src= "frameworks/player/primetimeei.min.js"></script> 
   <script src= "ExtCueOutContentFactory.js"></script>
   ```

1. Teste sua configuração.
