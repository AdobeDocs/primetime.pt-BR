---
description: O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/lineares.
title: Metadados do servidor e do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Visão geral {#primetime-ad-server-metadata-overview}

O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/lineares.

## Pré-requisito

Antes de incluir publicidade no seu conteúdo de vídeo, forneça as seguintes informações de metadados:

* Um `mediaID`, que identifica o conteúdo específico a ser reproduzido.
* Seu `zoneID`, que identifica sua empresa ou site.
* O domínio do servidor de publicidade, que especifica o domínio do servidor de publicidade atribuído.
* Outros parâmetros de definição de metas.

## Configurar metadados do servidor de anúncio do Primetime {#section_86C4A3B2DF124770B9B7FD2511394313}

Seu aplicativo deve fornecer ao TVSDK as informações `PTAuditudeMetadata` necessárias para se conectar ao servidor de publicidade.

Para configurar os metadados do servidor de publicidade:

1. Crie uma instância de [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) e defina suas propriedades.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Defina a instância `PTAuditudeMetadata` como metadados para os metadados `PTMediaPlayerItem` atuais usando `PTAdResolvingMetadataKey`.

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
