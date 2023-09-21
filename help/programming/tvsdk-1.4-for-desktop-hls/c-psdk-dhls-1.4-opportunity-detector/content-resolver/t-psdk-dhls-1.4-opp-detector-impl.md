---
description: Você pode implementar seus próprios detectores de oportunidade.
title: Implementar um detector de oportunidades personalizado
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Implementar um detector de oportunidades personalizado{#implement-a-custom-opportunity-detector}

Você pode implementar seus próprios detectores de oportunidade.

* Se o gerador de oportunidades estiver baseado em `TimedMetadata` objetos associados ao fluxo de mídia atual, ele deve estender a variável `SpliceOutOpportunityGenerator` ou `TimedMetadataOpportunityGenerator`.

* Se o gerador de oportunidades se basear em dados fora de banda fornecidos por um serviço externo (como um CIS), ele deverá estender a `OpportunityGenerator`.

1. Crie o gerador de oportunidades personalizado.

       Se o seu gerador de oportunidades personalizado for baseado em objetos &quot;TimedMetadata&quot;, estenda &quot;TimedMetadataOpportunityGenerator&quot; e substitua esses métodos:
   
   * `doConfigure` - Esse método é chamado após a criação do item do reprodutor de mídia e fornece ao gerador de oportunidades para criar um conjunto inicial de oportunidades, se necessário
   * `doProcess` - Este método é chamado sempre que um novo `TimedMetadata` for detectado (por exemplo, para fluxos ao vivo/lineares sempre que a lista de reprodução/manifesto for atualizada)

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

1. Crie a fábrica de conteúdo personalizado, que usa o gerador de oportunidades personalizado.

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

1. Registre a fábrica de conteúdo personalizado para que o fluxo de mídia seja reproduzido.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```
