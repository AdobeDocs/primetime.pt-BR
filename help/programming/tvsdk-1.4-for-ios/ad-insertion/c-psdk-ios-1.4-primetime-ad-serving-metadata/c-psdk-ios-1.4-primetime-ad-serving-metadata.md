---
description: O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/lineares.
title: Metadados do servidor e do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---


# Visão geral {#primetime-ad-server-metadata-overview}

O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/lineares.

>[!NOTE]
>
>Antes de incluir publicidade no seu conteúdo de vídeo, forneça as seguintes informações de metadados:
>
>* Um `mediaID`, que identifica o conteúdo específico a ser reproduzido.
>* Seu `zoneID`, que identifica sua empresa ou site.
>* O domínio do servidor de publicidade, que especifica o domínio do servidor de publicidade atribuído.
>* Outros parâmetros de definição de metas.

>



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

## Habilitar anúncios em reprodução de evento completo {#section_6016E1DAF03645C8A8388D03C6AB7571}

A repetição completa de evento (FER) é um ativo VOD que atua como um ativo ao vivo/DVR, portanto, o aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.

Para conteúdo ao vivo, o TVSDK usa os metadados/dicas no manifesto para determinar onde colocar anúncios. No entanto, às vezes, o conteúdo ao vivo/linear pode se assemelhar ao conteúdo VOD. Por exemplo, quando o conteúdo em tempo real é concluído, uma tag `EXT-X-ENDLIST` é anexada ao manifesto em tempo real. Para HLS, a tag `EXT-X-ENDLIST` significa que o fluxo é um fluxo de VOD. O TVSDK não pode diferenciar automaticamente esse fluxo de um fluxo de VOD normal para inserir anúncios corretamente.

Seu aplicativo deve informar ao TVSDK se o conteúdo é ao vivo ou VOD, especificando o `PTAdSignalingMode`.

Para um fluxo FER, o servidor de decisão do Adobe Primetime ad não deve fornecer a lista de ad breaks que precisam ser inseridos na linha do tempo antes de iniciar a reprodução. Esse é o processo típico do conteúdo VOD. Em vez disso, ao especificar um modo de sinalização diferente, o TVSDK lê todos os pontos de sinalização do manifesto FER e vai para o servidor de publicidade de cada ponto de sinalização para solicitar um ad break. Esse processo é semelhante ao conteúdo ao vivo/DVR.

Além de cada solicitação associada a um ponto de sinalização, o TVSDK faz uma solicitação de anúncio adicional para anúncios precedentes.

1. A partir de uma fonte externa, como o vCMS, obtenha o modo de sinalização que deve ser usado.
1. Crie os metadados relacionados à publicidade.
1. Se o comportamento padrão tiver de ser substituído, especifique o `PTAdSignalingMode` usando `PTAdMetadata.signalingMode`.

   Os valores válidos são `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues` e `PTAdSignalingModeServerMap`.

   Você deve definir o modo de sinalização de anúncio antes de chamar `prepareToPlay`. Depois que o TVSDK começa a resolver e colocar anúncios na linha do tempo, as alterações no modo de sinalização do anúncio são ignoradas. Defina o modo ao criar os metadados de anúncio do recurso.

1. Continue para a reprodução.

   ```
      PTMetadata *metadata = [[[PTMetadata alloc] init] autorelease]; 
   PTAuditudeMetadata *adMetadata = [[[PTAuditudeMetadata alloc] init] autorelease]; 
   adMetadata.zoneId = your-auditude-zone-id; 
   adMetadata.domain = @"your-auditude-domain"; 
   //adMetadata.enableDVRAds = YES; // FOR LIVE DVR case 
   //adMetadata.signalingMode = PTAdSignalingModeManifestCues;  
   // FOR VOD FER case 
   NSMutableDictionary *targetingParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [targetingParameters setValue:@"ipad" forKey:@"device"]; 
   [targetingParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.targetingParameters = targetingParameters; 
   NSMutableDictionary *customParameters = [[[NSMutableDictionary alloc] init] autorelease]; 
   [customParameters setValue:@"your-media-id" forKey:@"NW_ID"]; 
   [customParameters setValue:@"preroll" forKey:@"AD_OPPORTUNITY_ID"]; 
   adMetadata.customParameters = customParameters; 
   [metadata setMetadata:adMetadata forKey:PTAdResolvingMetadataKey]; 
   ```

