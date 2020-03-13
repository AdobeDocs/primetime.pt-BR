---
description: Você pode implementar seus próprios detectores de oportunidade.
seo-description: Você pode implementar seus próprios detectores de oportunidade.
seo-title: Implementar um detector de oportunidade personalizado
title: Implementar um detector de oportunidade personalizado
uuid: 18fb431b-4585-4293-92a7-b77ab7f9b7db
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Implementar um detector de oportunidade personalizado{#implement-a-custom-opportunity-detector}

Você pode implementar seus próprios detectores de oportunidade.

* Se o gerador de oportunidades for baseado em `TimedMetadata` objetos associados ao fluxo de mídia atual, ele deverá estender o `SpliceOutOpportunityGenerator` ou `TimedMetadataOpportunityGenerator`.

* Se o seu gerador de oportunidades for baseado em dados fora de banda fornecidos por um serviço externo (como um CIS), ele deverá estender o `OpportunityGenerator`.

1. Crie o gerador de oportunidades personalizado.

       Se o seu gerador de oportunidade personalizado for baseado em objetos TimedMetadata, estenda &quot;TimedMetadataOpportunityGenerator&quot; e substitua estes métodos:
   
   * `doConfigure` - Este método é chamado após a criação do item do player de mídia e oferece o gerador de oportunidades para criar um conjunto inicial de oportunidades, se necessário
   * `doProcess` - Este método é chamado sempre que novas `TimedMetadata` forem detectadas (por exemplo, para fluxos ao vivo/lineares toda vez que a lista de reprodução/manifesto for atualizado)

   ```
   public class CustomOpportunityGenerator extends TimedMetadataOpportunityGenerator { 
       override protected function doConfigure(playhead:Number, playbackRange:TimeRange):void { 
           // the playhead represents the initial playback position 
           // the playback range represents the initial playback range 
   
           // the item property indicates the current MediaPlayerItem associated with this generator 
           // the initial set of timed metadata can be obtain through the item property 
           var timedMetadataCollection:Vector.<TimedMetadata> = item.timedMetadata; 
       } 
   
       override protected function doProcess(timedMetadata:TimedMetadata):void { 
           ... 
   
           // when an opportunity is created by this generator 
           // we need to notify the TVSDK through the client property 
           client.resolve(opportunity); 
       }  
       ... 
   }
   ```

1. Crie a fábrica de conteúdo personalizada, que usa o gerador de oportunidade personalizado.

   ```
   public class CustomContentFactory extends DefaultContentFactory { 
       ... 
   
       /** 
       * @inheritDoc 
       */ 
       override protected function doRetrieveGenerators(item:MediaPlayerItem):Vector.<OpportunityGenerator> { 
           var result:Vector.<OpportunityGenerator> = new Vector.<OpportunityGenerator>(); 
           result.push(new CustomOpportunityGenerator()); 
   
           return result; 
       } 
   }
   ```

1. Registre a fábrica de conteúdo personalizado para o fluxo de mídia a ser reproduzido.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

