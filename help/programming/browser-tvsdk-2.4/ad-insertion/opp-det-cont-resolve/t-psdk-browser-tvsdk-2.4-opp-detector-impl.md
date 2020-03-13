---
description: Você pode implementar seu próprio gerador de oportunidades estendendo a interface OpportunityGenerator.
seo-description: Você pode implementar seu próprio gerador de oportunidades estendendo a interface OpportunityGenerator.
seo-title: Implementar um gerador de oportunidade personalizado
title: Implementar um gerador de oportunidade personalizado
uuid: b80da2da-32d5-41f7-86ca-936d6f25b015
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementar um gerador de oportunidade personalizado{#implement-a-custom-opportunity-generator}

Você pode implementar seu próprio gerador de oportunidades estendendo a interface OpportunityGenerator.

1. Crie o gerador de oportunidades personalizado.

   Por exemplo:

   ```js
   /** 
   * Class implementing AdobePSDK.OpportunityGenerator interface 
   */ 
   CustomOpportunityGenerator = function () { 
   }; 
   
   CustomOpportunityGenerator.prototype = { 
       constructor: CustomOpportunityGenerator, 
       configureCallbackFunc: function (item, client, mode, playhead, playbackRange) {  
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current AdobePSDK.MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadatas = item.timedMetadata; 
       }, 
       updateCallbackFunc: function (playhead, playbackRange) { 
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve (opportunity); 
       }, 
       … 
   }; 
   ```

1. Crie a fábrica de conteúdo personalizada, que usa o gerador de oportunidade personalizado.

   Por exemplo:

   ```js
   /** 
     * Class implementing AdobePSDK.ContentFactory interface 
   */ 
   CustomContentFactory = function () { 
   }; 
   
   CustomContentFactory.prototype = { 
          constructor: CustomContentFactory, 
          retrieveOpportunityGeneratorsCallbackFunc: function (item) { 
               var result = []; 
               result.push (new CustomOpportunityGenerator()); 
               return result; 
       }, 
       … 
   }; 
   ```

1. Registre a fábrica de conteúdo personalizado para o fluxo de mídia a ser reproduzido.

   No player da UI Framework, você pode especificar a fábrica de conteúdo personalizado da seguinte maneira:

   ```js
   var advertisingFactory = new CustomContentFactory(); 
   var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
           mediaPlayerItemConfig: { 
                   advertisingFactory: advertisingFactory 
           }, 
               mediaResource: { 
                   resourceUrl:'Specify Resource Url' 
          } 
     } 
   }); 
   ```

