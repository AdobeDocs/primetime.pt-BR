---
description: O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/linear.
seo-description: O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/linear.
seo-title: Metadados do Primetime e do servidor
title: Metadados do Primetime e do servidor
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 9d60bff4035963572e49fa49effa576ca854f799
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Visão geral {#primetime-ad-server-metadata-overview}

O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/linear.

## Pré-requisito

Antes de incluir publicidade no conteúdo de vídeo, forneça as seguintes informações de metadados:

* A, que identifica o conteúdo específico a ser reproduzido. `mediaID`
* Seu `zoneID`, que identifica sua empresa ou site.
* O domínio do servidor de publicidade, que especifica o domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

## Configurar metadados do servidor e do Primetime {#section_86C4A3B2DF124770B9B7FD2511394313}

Seu aplicativo deve fornecer ao TVSDK as informações necessárias `PTAuditudeMetadata` para se conectar ao servidor de anúncios.

Para configurar os metadados do servidor de publicidade:

1. Crie uma instância de [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) e defina suas propriedades.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Defina a `PTAuditudeMetadata` instância como metadados para os `PTMediaPlayerItem` metadados atuais usando `PTAdResolvingMetadataKey`.

   ```
   // Metadata is an instance of PTMetadata that is used to create the PTMediaPlayerItem 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey];  
   [adMetadata release];
   ```

   Veja um exemplo:

   ```
   PTMetadata *metadata = [self createMetadata]; 
   PTMediaPlayerItem *item =  
     [[[PTMediaPlayerItem alloc] initWithUrl:url mediaId:yourMediaID metadata:metadata] autorelease]; 
   
   - (PTMetadata *) createMetadata { 
       PTMetadata* metadata = [[[PTMetadata alloc] init] autorelease]; 
   
       PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease];  
       adMetadata.zoneId = yourZoneID; 
       adMetadata.domain = yourAdServerDomain; 
   
       [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   
       return metadata; 
   }
   ```
