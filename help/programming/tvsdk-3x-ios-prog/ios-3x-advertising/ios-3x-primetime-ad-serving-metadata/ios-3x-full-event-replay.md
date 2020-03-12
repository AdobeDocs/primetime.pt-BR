---
description: O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/linear.
seo-description: O TVSDK oferece suporte à resolução e inserção de anúncios para fluxos VOD e live/linear.
seo-title: Metadados do Primetime e do servidor
title: Metadados do Primetime e do servidor
uuid: 61e224dd-551a-438f-8560-e64915087fef
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Habilitar anúncios em repetição de evento completo {#section_6016E1DAF03645C8A8388D03C6AB7571}

A repetição completa de eventos (FER) é um ativo VOD que atua como um ativo ao vivo/DVR, portanto, seu aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.

Para conteúdo ao vivo, o TVSDK usa os metadados/dicas no manifesto para determinar onde os anúncios devem ser colocados. No entanto, às vezes o conteúdo ao vivo/linear pode se assemelhar ao conteúdo VOD. Por exemplo, quando o conteúdo em tempo real é concluído, uma `EXT-X-ENDLIST` tag é anexada ao manifesto em tempo real. Para HLS, a `EXT-X-ENDLIST` tag significa que o fluxo é um fluxo VOD. O TVSDK não pode diferenciar automaticamente esse fluxo de um fluxo VOD normal para inserir corretamente os anúncios.

Seu aplicativo deve informar ao TVSDK se o conteúdo é ao vivo ou VOD ao especificar o `PTAdSignalingMode`.

Para um fluxo FER, o servidor de decisão de anúncio do Adobe Primetime não deve fornecer a lista de quebras de anúncio que precisam ser inseridas na linha do tempo antes de iniciar a reprodução. Esse é o processo típico para conteúdo VOD. Em vez disso, ao especificar um modo de sinalização diferente, o TVSDK lê todos os pontos de sinalização do manifesto FER e vai para o servidor de anúncios para cada ponto de sinalização para solicitar uma pausa de anúncio. Esse processo é semelhante ao conteúdo ao vivo/DVR.

Além de cada solicitação associada a um ponto de sinalização, o TVSDK faz uma solicitação de anúncio adicional para anúncios precedentes.

1. A partir de uma fonte externa, como o vCMS, obtenha o modo de sinalização que deve ser usado.
1. Crie os metadados relacionados ao anúncio.
1. Se o comportamento padrão precisar ser substituído, especifique o comportamento `PTAdSignalingMode` usando `PTAdMetadata.signalingMode`.

   Os valores válidos são `PTAdSignalingModeDefault`, `PTAdSignalingModeManifestCues`e `PTAdSignalingModeServerMap`.

   Você deve definir o modo de sinalização de anúncio antes de chamar `prepareToPlay`. Depois que o TVSDK começar a resolver e colocar anúncios na linha do tempo, as alterações no modo de sinalização do anúncio serão ignoradas. Defina o modo ao criar os metadados de publicidade para o recurso.

1. Continue com a reprodução.

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
