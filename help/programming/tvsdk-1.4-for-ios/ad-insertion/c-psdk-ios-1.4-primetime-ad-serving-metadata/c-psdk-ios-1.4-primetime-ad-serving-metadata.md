---
description: O TVSDK é compatível com a resolução e inserção de anúncios para VOD e fluxos dinâmicos/lineares.
title: Metadados do servidor de publicidade do Primetime
exl-id: 3723dd2f-292c-4ce5-9670-fda1b1f2b5df
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 0%

---

# Visão geral {#primetime-ad-server-metadata-overview}

O TVSDK é compatível com a resolução e inserção de anúncios para VOD e fluxos dinâmicos/lineares.

>[!NOTE]
>
>Antes de incluir publicidade no conteúdo de vídeo, forneça as seguintes informações de metadados:
>
>* A `mediaID`, que identifica o conteúdo específico a ser reproduzido.
>* Seu `zoneID`, que identifica a empresa ou o site.
>* O domínio do servidor de publicidade, que especifica o domínio do servidor de publicidade atribuído.
>* Outros parâmetros de direcionamento.
>


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

## Ativar anúncios na repetição completa do evento {#section_6016E1DAF03645C8A8388D03C6AB7571}

A repetição de evento completo (FER) é um ativo de VOD que atua como um ativo ao vivo/DVR, portanto, seu aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.

Para conteúdo ao vivo, o TVSDK usa os metadados/dicas no manifesto para determinar onde colocar os anúncios. No entanto, às vezes, o conteúdo dinâmico/linear pode se parecer com o conteúdo VOD. Por exemplo, quando o conteúdo ativo é concluído, uma variável `EXT-X-ENDLIST` tag é anexada ao manifesto em tempo real. Para a HLS, a variável `EXT-X-ENDLIST` tag significa que o fluxo é um fluxo de VOD. O TVSDK não consegue diferenciar automaticamente esse fluxo de um fluxo de VOD normal para inserir anúncios corretamente.

Seu aplicativo deve informar ao TVSDK se o conteúdo é em tempo real ou VOD, especificando o `PTAdSignalingMode`.

Para um fluxo de FER, o servidor de decisão de anúncios do Adobe Primetime não deve fornecer a lista de ad breaks que precisam ser inseridos na linha do tempo antes de iniciar a reprodução. Esse é o processo normal para o conteúdo de VOD. Em vez disso, ao especificar um modo de sinalização diferente, o TVSDK lê todos os pontos de sinalização do manifesto FER e vai para o servidor de publicidade para cada ponto de sinalização para solicitar um ad break. Esse processo é semelhante ao conteúdo live/DVR.

Além de cada solicitação associada a um ponto de sinalização, o TVSDK faz uma solicitação de anúncio adicional para anúncios precedentes.

1. A partir de uma fonte externa, como vCMS, obtenha o modo de sinalização que deve ser usado.
1. Crie os metadados relacionados à publicidade.
1. Se o comportamento padrão precisar ser substituído, especifique o `PTAdSignalingMode` usando `PTAdMetadata.signalingMode`.

   Os valores válidos são `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`, e `PTAdSignalingModeServerMap`.

   Você deve definir o modo de sinalização de anúncios antes de chamar `prepareToPlay`. Depois que o TVSDK começa a resolver e colocar anúncios na linha do tempo, as alterações no modo de sinalização de anúncios são ignoradas. Defina o modo ao criar os metadados de publicidade para o recurso.

1. Prossiga para a reprodução.

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
