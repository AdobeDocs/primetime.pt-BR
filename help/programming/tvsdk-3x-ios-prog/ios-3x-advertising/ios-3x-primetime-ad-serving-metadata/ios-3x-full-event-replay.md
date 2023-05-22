---
description: O TVSDK é compatível com a resolução e inserção de anúncios para VOD e fluxos dinâmicos/lineares.
title: Metadados do servidor de publicidade do Primetime
exl-id: 32813029-51d4-421e-8278-a2d42c59e4dc
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Ativar anúncios na repetição completa do evento {#section_6016E1DAF03645C8A8388D03C6AB7571}

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
