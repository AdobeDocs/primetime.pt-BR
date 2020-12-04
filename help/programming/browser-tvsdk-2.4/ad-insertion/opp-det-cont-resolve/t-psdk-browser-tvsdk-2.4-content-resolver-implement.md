---
description: Você pode implementar seus próprios resolvedores de conteúdo com base nos resolvedores padrão.
seo-description: Você pode implementar seus próprios resolvedores de conteúdo com base nos resolvedores padrão.
seo-title: Implementar um resolvedor de conteúdo personalizado
title: Implementar um resolvedor de conteúdo personalizado
uuid: cf85dd90-242e-4f9e-9785-158ca0fc9465
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Implementar um resolvedor de conteúdo personalizado{#implement-a-custom-content-resolver}

Você pode implementar seus próprios resolvedores de conteúdo com base nos resolvedores padrão.

Quando o TVSDK do navegador detecta uma nova oportunidade, ele é repetido pelos resolvedores de conteúdo registrados procurando por um que seja capaz de resolver essa oportunidade usando o método `canResolve`. O primeiro que retornar verdadeiro é selecionado para resolver a oportunidade. Se nenhum resolvedor de conteúdo for capaz, essa oportunidade será ignorada. Como o processo de resolução de conteúdo geralmente é assíncrono, o resolvedor de conteúdo é responsável por notificar o TVSDK do navegador quando o processo é concluído.

Lembre-se das seguintes informações:

* O resolvedor de conteúdo chama `client.process` para especificar qual operação de linha do tempo o TVSDK precisa executar.

   A operação geralmente é uma disposição de pausa de anúncio.

* O resolvedor de conteúdo chama `client.notifyCompleted` se o processo de resolução for bem-sucedido ou `client.notifyFailed` se o processo falhar.

1. Crie um resolvedor de oportunidades personalizado.

   ```js
   /** 
     * Class implementing AdobePSDK.ContentResolver interface  
   */ 
   CustomResolver = function () { 
   }; 
   
   CustomResolver.prototype = { 
       constructor: CustomResolver, 
       configureCallbackFunc: function (item, client) { 
       // here you can read any media stream characteristics which 
       // might help configure your content resolver like 
       // - the media player item configuration through the item.config 
       // - the media resource metadata through item.resource.metadata 
      }, 
   
       canResolveCallbackFunc: function (opportunity) { 
       // check if the opportunity can be resolved by this resolver 
       // if yes return true, otherwise return false 
       return true; 
      }, 
   
       resolveCallbackFunc: function (opportunity) {         
       // start the resolving process 
       // communicate with your custom ad server 
   
       // in this example we assume that: 
       // - if successful, onResolveCompleted method will be invoked 
       // - if failed, onResolveFailed method will be invoked 
      }, 
   
       onResolveCompleted: function (response) { 
        try { 
           var proposals = []; 
           // extract the timeline ad placement from the response 
           // and add them to the proposal vector 
           // - extract the ad break 
           // - calculate the placement (can reuse the _opportunity.placement) 
           // var timelineOperation = new AdobePSDK.AdBreakPlacement (adBreak, placement); 
           // proposals.push (timelineOperation); 
   
           client.process (proposals); 
           client.notifyCompleted (_opportunity); 
       } catch (error) { 
           onResolveFailed (error); 
       } 
   }, 
   
       onResolveFailed: function (error) { 
         client.notifyFailed (_opportunity); 
       } 
   
   }; 
   ```

1. Crie a fábrica de conteúdo personalizada, que usa o resolvedor de conteúdo personalizado.

   Por exemplo:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
       constructor: CustomContentFactory, 
       retrieveResolversCallbackFunc: function (item) { 
           var result = []; 
           var resource = item.resource; 
           if (resource.metadata.containsKey("custom-opportunity-detector")) { 
               result.push (new CustomResolver()); 
           } 
           return result; 
       }, 
       … 
   }; 
   ```

1. Registre a fábrica de conteúdo personalizado para o fluxo de mídia a ser reproduzido.

   No player da UI Framework, você pode especificar a fábrica de conteúdo personalizado da seguinte maneira:

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var advertisingMetadata = new AdobePSDK.AdvertisingMetadata(); 
   // set any parameter you need for custom ad resolver 
   // advertisingMetadata.setValue ("customparam", "customvalue"); 
   
   var metadata = new AdobePSDK.Metadata(); 
   metadata.setMetadata ("custom-opportunity-detector", advertisingMetadata); 
   
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
       mediaPlayerItemConfig: { 
              advertisingFactory: advertisingFactory 
       }, 
          mediaResource: { 
                  resourceUrl:'Specify Resource Url', 
                  metadata: metadata 
          } 
   } 
   
   }); 
   ```

