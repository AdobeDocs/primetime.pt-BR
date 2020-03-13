---
description: A repetição completa de eventos (FER) é um ativo VOD que atua como um ativo ao vivo/DVR, portanto, seu aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.
seo-description: A repetição completa de eventos (FER) é um ativo VOD que atua como um ativo ao vivo/DVR, portanto, seu aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.
seo-title: Habilitar anúncios em repetição de evento completo
title: Habilitar anúncios em repetição de evento completo
uuid: 70e463bd-332c-4f91-ac05-03e79c0939a4
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Habilitar anúncios em repetição de evento completo{#enable-ads-in-full-event-replay}

A repetição completa de eventos (FER) é um ativo VOD que atua como um ativo ao vivo/DVR, portanto, seu aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.

Para conteúdo ao vivo, o TVSDK usa os metadados/dicas no manifesto para determinar onde os anúncios devem ser colocados. No entanto, às vezes o conteúdo ao vivo/linear pode se assemelhar ao conteúdo VOD. Por exemplo, quando o conteúdo em tempo real é concluído, uma `EXT-X-ENDLIST` tag é anexada ao manifesto em tempo real. Para HLS, a `EXT-X-ENDLIST` tag significa que o fluxo é um fluxo VOD. O TVSDK não pode diferenciar automaticamente esse fluxo de um fluxo VOD normal para inserir corretamente os anúncios.

Seu aplicativo deve informar ao TVSDK se o conteúdo é ao vivo ou VOD ao especificar o `AdSignalingMode`.

Para um fluxo FER, o servidor de decisão de anúncio do Adobe Primetime não deve fornecer a lista de quebras de anúncio que precisam ser inseridas na linha do tempo antes de iniciar a reprodução. Esse é o processo típico para conteúdo VOD. Em vez disso, ao especificar um modo de sinalização diferente, o TVSDK lê todos os pontos de sinalização do manifesto FER e vai para o servidor de anúncios para cada ponto de sinalização para solicitar uma pausa de anúncio. Esse processo é semelhante ao conteúdo ao vivo/DVR.

Além de cada solicitação associada a um ponto de sinalização, o TVSDK faz uma solicitação de anúncio adicional para anúncios precedentes.

1. A partir de uma fonte externa, como o vCMS, obtenha o modo de sinalização que deve ser usado.
1. Crie os metadados relacionados ao anúncio.
1. Se o comportamento padrão precisar ser substituído, especifique o comportamento `AdSignalingMode` usando `AdvertisingMetadata.setSignalingMode`.

   Os valores válidos são `DEFAULT, SERVER_MAP`e `MANIFEST_CUES`.

   Você deve definir o modo de sinalização de anúncio antes de chamar `prepareToPlay`. Depois que o TVSDK começar a resolver e colocar anúncios na linha do tempo, as alterações no modo de sinalização do anúncio serão ignoradas. Defina o modo ao criar o `AuditudeSettings` objeto.

1. Continue com a reprodução.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->

