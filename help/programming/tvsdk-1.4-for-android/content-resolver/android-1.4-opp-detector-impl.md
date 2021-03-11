---
description: Você pode implementar seus próprios detectores de oportunidade implementando a interface PlacementOpportunityDetector.
title: Implementar um detector de oportunidade personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 2%

---


# Implementar um detector de oportunidade personalizado {#implement-a-custom-opportunity-detector}

Você pode implementar seus próprios detectores de oportunidade implementando a interface PlacementOpportunityDetector.

1. Crie uma instância `AdvertisingFactory` personalizada e substitua `createOpportunityDetector`. Por exemplo:

   ```java
   new AdvertisingFactory() { 
       ... 
       @Override 
       public PlacementOpportunityDetector createOpportunityDetector(MediaPlayerItem item) { 
           return new CustomPlacementOpportunityDetector(); 
       } 
       ... 
   }
   ```

1. Registre a fábrica do cliente de anúncio no `MediaPlayer`. Por exemplo:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Crie uma classe de detector de oportunidade personalizada que estende a classe `PlacementOpportunityDetector`.
   1. No detector de oportunidade personalizado, substitua essa função:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      O `timedMetadataList` contém a lista de `TimedMetadata` disponíveis, que é classificada. Os metadados contêm os parâmetros de definição de metas e os parâmetros personalizados a serem enviados ao provedor de anúncios.

   1. Para cada `TimedMetadata`, crie um `List<PlacementOpportunity>`. A lista pode estar vazia, mas não nula. `PlacementOpportunity` deve ter os seguintes atributos:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Após criar oportunidades de posicionamento para todos os objetos de metadados cronometrados detectados, basta retornar a lista `PlacementOpportunity`.

Este é um exemplo de detector de oportunidade de posicionamento personalizado:

```java
public class CustomPlacementOpportunityDetector implements PlacementOpportunityDetector { 
    ... 
    @Override 
    public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata) { 
        ... 
        List<PlacementOpportunity> opportunities = new ArrayList<PlacementOpportunity>(); 
 
        for (TimedMetadata timedMetadata : timedMetadataList) { 
 
            if (isOpportunity(timedMetadata)) {        // check if given timedMetadata should be  
                                                       // considered as an opportunity 
 
                // create an object of PlacementOpportunity and add it to the opportunities list 
                PlacementOpportunity opportunity =  
                  createPlacementOpportunity(timedMetadata, airingId, metadata); 
                Opportunities.add(opportunity); 
            } 
        } 
        return opportunities; 
    }    
    ... 
} 
```

