---
description: A repetição completa de evento (FER) é um ativo VOD que atua como um ativo ao vivo/DVR, portanto, o aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.
title: Habilitar anúncios em reprodução de evento completo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---


# Habilitar anúncios em reprodução de evento completo{#enable-ads-in-full-event-replay}

A repetição completa de evento (FER) é um ativo VOD que atua como um ativo ao vivo/DVR, portanto, o aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.

Para conteúdo ao vivo, o TVSDK usa os metadados/dicas no manifesto para determinar onde colocar anúncios. No entanto, às vezes, o conteúdo ao vivo/linear pode se assemelhar ao conteúdo VOD. Por exemplo, quando o conteúdo em tempo real é concluído, uma tag `EXT-X-ENDLIST` é anexada ao manifesto em tempo real. Para HLS, a tag `EXT-X-ENDLIST` significa que o fluxo é um fluxo de VOD. O TVSDK não pode diferenciar automaticamente esse fluxo de um fluxo de VOD normal para inserir anúncios corretamente.

Seu aplicativo deve informar ao TVSDK se o conteúdo é ao vivo ou VOD, especificando o `AdSignalingMode`.

Para um fluxo FER, o servidor de decisão do Adobe Primetime ad não deve fornecer a lista de ad breaks que precisam ser inseridos na linha do tempo antes de iniciar a reprodução. Esse é o processo típico do conteúdo VOD. Em vez disso, ao especificar um modo de sinalização diferente, o TVSDK lê todos os pontos de sinalização do manifesto FER e vai para o servidor de publicidade de cada ponto de sinalização para solicitar um ad break. Esse processo é semelhante ao conteúdo ao vivo/DVR.

Além de cada solicitação associada a um ponto de sinalização, o TVSDK faz uma solicitação de anúncio adicional para anúncios precedentes.

1. A partir de uma fonte externa, como o vCMS, obtenha o modo de sinalização que deve ser usado.
1. Crie os metadados relacionados à publicidade.
1. Se o comportamento padrão tiver de ser substituído, especifique o `AdSignalingMode` usando `AdvertisingMetadata.setSignalingMode`.

   Os valores válidos são `DEFAULT, SERVER_MAP` e `MANIFEST_CUES`.

   Você deve definir o modo de sinalização de anúncio antes de chamar `prepareToPlay`. Depois que o TVSDK começa a resolver e colocar anúncios na linha do tempo, as alterações no modo de sinalização do anúncio são ignoradas. Defina o modo ao criar o objeto `AuditudeSettings`.

1. Continue para a reprodução.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

