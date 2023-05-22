---
description: O TVSDK é compatível com a resolução e inserção de anúncios para VOD e fluxos dinâmicos/lineares.
title: Metadados do servidor de publicidade do Primetime
exl-id: f27657ac-4037-45e5-a658-ad9a783dd990
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---

# Visão geral {#primetime-ad-server-metadata-overview}

O TVSDK é compatível com a resolução e inserção de anúncios para VOD e fluxos dinâmicos/lineares.

## Pré-requisito

Antes de incluir publicidade no conteúdo de vídeo, forneça as seguintes informações de metadados:

* A `mediaID`, que identifica o conteúdo específico a ser reproduzido.
* Seu `zoneID`, que identifica a empresa ou o site.
* O domínio do servidor de publicidade, que especifica o domínio do servidor de publicidade atribuído.
* Outros parâmetros de direcionamento.

## Configurar metadados do Primetime e do servidor {#section_86C4A3B2DF124770B9B7FD2511394313}

Seu aplicativo deve fornecer ao TVSDK os dados necessários `PTAuditudeMetadata` informações para se conectar ao servidor de publicidade.

Para configurar os metadados do servidor de publicidade:

1. Criar uma instância de [PTAuditudeMetadata](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAuditudeMetadata.html) e defina suas propriedades.

   ```
   PTAuditudeMetadata *adMetadata = [[PTAuditudeMetadata alloc] init];  
   adMetadata.zoneId = @"INSERT_YOUR_ZONE_ID_HERE"; 
   adMetadata.domain = @"INSERT_YOUR_DOMAIN_HERE"; 
   // Optionally set user agent 
   adMetadata.userAgent = @"INSERT_AGENT_NAME_HERE; 
   ```

1. Defina o `PTAuditudeMetadata` instância como metadados para a atual `PTMediaPlayerItem` metadados usando `PTAdResolvingMetadataKey`.

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
