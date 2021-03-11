---
description: Você pode implementar seus próprios detectores de oportunidade.
title: Implementar um detector de oportunidade personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---


# Implementar um detector de oportunidade personalizado{#implement-a-custom-opportunity-detector}

Você pode implementar seus próprios detectores de oportunidade.

* Se o gerador de oportunidades for baseado em `TimedMetadata` objetos associados ao fluxo de mídia atual, ele deverá estender o `SpliceOutOpportunityGenerator` ou `TimedMetadataOpportunityGenerator`.

* Se o seu gerador de oportunidades se baseia em dados fora de banda fornecidos por um serviço externo (como um CIS), então ele deve estender o `OpportunityGenerator`.

1. Crie o gerador de oportunidade personalizado.

       Se o seu gerador de oportunidade personalizado se baseia em objetos &quot;TimedMetadata&quot;, estenda &quot;TimedMetadataOpportunityGenerator&quot; e substitua esses métodos:
   
   * `doConfigure` - Este método é chamado depois que o item do reprodutor de mídia é criado e fornece o gerador de oportunidades para criar um conjunto inicial de oportunidades, se necessário
   * `doProcess` - Esse método é chamado sempre que  `TimedMetadata` for detectado novo (por exemplo, para fluxos ao vivo/lineares toda vez que a lista de reprodução/manifesto for atualizada)

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

1. Crie a fábrica de conteúdo personalizado, que usa o gerador de oportunidade personalizado.

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

1. Registre a fábrica de conteúdo personalizado do fluxo de mídia a ser reproduzido.

   ```
   var mediaPlayerItemConfig:MediaPlayerItemConfig = new DefaultMediaPlayerItemConfig(); 
   mediaPlayerItemConfig.advertisingFactory = new CustomContentFactory(); 
   ... 
   
   player.replaceCurrentResource(mediaResource, mediaPlayerItemConfig);
   ```

