---
description: Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK do navegador escute eventos relacionados a anúncios.
seo-description: Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK do navegador escute eventos relacionados a anúncios.
seo-title: Exibir anúncios em banners
title: Exibir anúncios em banners
uuid: aabc126e-b3aa-42dd-ab50-a7db8e324c50
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '264'
ht-degree: 0%

---


# Exibir anúncios em banners {#display-banner-ads}

Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK do navegador escute eventos relacionados a anúncios.

O TVSDK do navegador fornece uma lista de anúncios de banner associados a um anúncio linear por meio do evento `AdobePSDK.PSDKEventType.AD_STARTED`.

Os manifestos podem especificar anúncios de banner companheiro:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou um arquivo SWF de Flash Adobe

Para cada anúncio complementar, o TVSDK do navegador indica quais tipos estão disponíveis para seu aplicativo.

Adicione um ouvinte para o evento `AdobePSDK.PSDKEventType.AD_STARTED` que faz o seguinte:
1. Limpa os anúncios existentes na instância do banner.
1. Obtém a lista de anúncios complementares de `Ad.getCompanionAssets`.
1. Se a lista de anúncios complementares não estiver vazia, repita a lista para ver as instâncias de banner.

   Cada instância do banner (um `AdBannerAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
1. Se um anúncio de vídeo não tiver anúncios adicionais reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.
1. Envia as informações do banner para uma função na sua página que exibe os banners em um local apropriado.

   Geralmente é um `div`, e sua função usa `div ID` para exibir o banner. Por exemplo:

   Adicione o ouvinte do evento:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implemente o manipulador do listener:

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

