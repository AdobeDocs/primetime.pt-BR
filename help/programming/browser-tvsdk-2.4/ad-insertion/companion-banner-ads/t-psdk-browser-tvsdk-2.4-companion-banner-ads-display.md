---
description: Para exibir anúncios de banner, você precisa criar instâncias de banner e permitir que o TVSDK do navegador acompanhe eventos relacionados a anúncios.
title: Exibir anúncios de banner
exl-id: 331c10a4-ae31-4d3b-aaca-9497e2970ecf
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '242'
ht-degree: 0%

---

# Exibir anúncios de banner {#display-banner-ads}

Para exibir anúncios de banner, você precisa criar instâncias de banner e permitir que o TVSDK do navegador acompanhe eventos relacionados a anúncios.

O TVSDK do navegador fornece uma lista de anúncios de banner complementares associados a um anúncio linear por meio do `AdobePSDK.PSDKEventType.AD_STARTED` evento.

Os manifestos podem especificar anúncios de banner complementares por:

* Um trecho de HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou de um arquivo SWF de Adobe Flash

Para cada anúncio complementar, o TVSDK do navegador indica quais tipos estão disponíveis para seu aplicativo.

Adicionar um ouvinte para o evento `AdobePSDK.PSDKEventType.AD_STARTED` que faz o seguinte:
1. Limpa os anúncios existentes na instância do banner.
1. Obtém a lista de anúncios complementares de `Ad.getCompanionAssets`.
1. Se a lista de anúncios complementares não estiver vazia, repita sobre a lista para instâncias de banner.

   Cada instância do banner (uma `AdBannerAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
1. Se um anúncio de vídeo não tiver anúncios complementares reservados com ele, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.
1. Envia as informações do banner para uma função na página que exibe os banners no local apropriado.

   Isso geralmente é um `div`, e sua função usa o `div ID` para exibir o banner. Por exemplo:

   Adicione o ouvinte de eventos:

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
