---
description: Você pode implementar seus próprios detectores de oportunidade implementando a interface PlacementOpportunityDetector.
title: Implementar um detector de oportunidades personalizado
exl-id: d78949a0-2c76-4976-9358-05f3db86781e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Implementar um detector de oportunidades personalizado {#implement-a-custom-opportunity-detector}

Você pode implementar seus próprios detectores de oportunidade implementando a interface PlacementOpportunityDetector.

1. Criar um personalizado `AdvertisingFactory` instância e substituição `createOpportunityDetector`. Por exemplo:

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

1. Registre a fábrica de clientes de anúncios na `MediaPlayer`. Por exemplo:

   ```java
   // register the custom advertising factory with media player 
   advertisingFactory = createCustomAdvertisingFactory(); 
   mediaPlayer.registerAdClientFactory(advertisingFactory);
   ```

1. Criar uma classe de detector de oportunidade personalizada que estende a `PlacementOpportunityDetector` classe.
   1. No detector de oportunidade personalizado, substitua esta função:

      ```java
      public List<PlacementOpportunity> process(List<TimedMetadata> timedMetadataList, Metadata metadata)
      ```

      A variável `timedMetadataList` contém a lista de opções disponíveis `TimedMetadata`, que é classificado. Os metadados contêm os parâmetros de direcionamento e os parâmetros personalizados a serem enviados ao provedor de anúncios.

   1. Para cada `TimedMetadata`, criar um `List<PlacementOpportunity>`. A lista pode estar vazia, mas não ser nula. `PlacementOpportunity` deve ter os seguintes atributos:

      ```java
      PlacementOpportunity( 
          String id,                                      // can be id from timedMetadata 
          PlacementInformation placementInformation   // PlacementInformation object containing Type, time, duration 
          Metadata metadata                           // ad metadata containing targeting params sent to the ad provider 
      )
      ```

   1. Depois que as oportunidades de posicionamento forem criadas para todos os objetos de metadados cronometrados detectados, basta retornar a `PlacementOpportunity` lista.

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
