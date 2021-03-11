---
description: Para exibir anúncios de banner, é necessário criar instâncias de banner e permitir que o TVSDK do navegador acompanhe eventos relacionados a anúncios.
title: Exibir anúncios de banner
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---


# Exibir anúncios de banner {#display-banner-ads}

Para exibir anúncios de banner, é necessário criar instâncias de banner e permitir que o TVSDK do navegador acompanhe eventos relacionados a anúncios.

O TVSDK do navegador fornece uma lista de anúncios de banner complementar associados a um anúncio linear por meio do evento `AdobePSDK.PSDKEventType.AD_STARTED`.

Os manifestos podem especificar anúncios de banner complementar ao:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou um arquivo SWF de Flash Adobe

Para cada anúncio complementar, o TVSDK do navegador indica quais tipos estão disponíveis para seu aplicativo.

Adicione um ouvinte para o evento `AdobePSDK.PSDKEventType.AD_STARTED` que faz o seguinte:
1. Apaga anúncios existentes na instância do banner.
1. Obtém a lista de anúncios complementares de `Ad.getCompanionAssets`.
1. Se a lista de anúncios complementares não estiver vazia, passe o mouse sobre a lista para as instâncias de banner.

   Cada instância de banner (um `AdBannerAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
1. Se um anúncio de vídeo não tiver anúncios complementares reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.
1. Envia as informações do banner para uma função na página que exibe os banners em um local apropriado.

   Geralmente é um `div`, e sua função usa o `div ID` para exibir o banner. Por exemplo:

   Adicione o ouvinte do evento:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implemente o manipulador do ouvinte:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void 
   { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
            for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
                } 
            } 
        }  
        //...        
   }
   ```

   Exemplo de JavaScript para lidar com a exibição:

   ```js
   function displayCompanion (resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
       var bannerDiv = document.getElementById('banner' + width + 'x' + height);  
   
       // Assuming that there is an HTML element on the page  
       // with an id of "banner300x250", for example 
       if (bannerDiv !== null) { 
           bannerDiv.innerHTML = data; 
       } 
   }
   ```

