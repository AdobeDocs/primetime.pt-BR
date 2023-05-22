---
description: A repetição de evento completo (FER) é um ativo de VOD que atua como um ativo ao vivo/DVR, portanto, seu aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.
title: Ativar anúncios na repetição completa do evento
exl-id: d6f7efc9-48f4-4101-a425-c354557cdd4c
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Ativar anúncios na repetição completa do evento{#enable-ads-in-full-event-replay}

A repetição de evento completo (FER) é um ativo de VOD que atua como um ativo ao vivo/DVR, portanto, seu aplicativo deve tomar medidas para garantir que os anúncios sejam colocados corretamente.

Para conteúdo ao vivo, o TVSDK usa os metadados/dicas no manifesto para determinar onde colocar os anúncios. No entanto, às vezes, o conteúdo dinâmico/linear pode se parecer com o conteúdo VOD. Por exemplo, quando o conteúdo ativo é concluído, uma variável `EXT-X-ENDLIST` tag é anexada ao manifesto em tempo real. Para a HLS, a variável `EXT-X-ENDLIST` tag significa que o fluxo é um fluxo de VOD. O TVSDK não consegue diferenciar automaticamente esse fluxo de um fluxo de VOD normal para inserir anúncios corretamente.

Seu aplicativo deve informar ao TVSDK se o conteúdo é em tempo real ou VOD, especificando o `AdSignalingMode`.

Para um fluxo de FER, o servidor de decisão de anúncios do Adobe Primetime não deve fornecer a lista de ad breaks que precisam ser inseridos na linha do tempo antes de iniciar a reprodução. Esse é o processo normal para o conteúdo de VOD. Em vez disso, ao especificar um modo de sinalização diferente, o TVSDK lê todos os pontos de sinalização do manifesto FER e vai para o servidor de publicidade para cada ponto de sinalização para solicitar um ad break. Esse processo é semelhante ao conteúdo live/DVR.

Além de cada solicitação associada a um ponto de sinalização, o TVSDK faz uma solicitação de anúncio adicional para anúncios precedentes.

1. A partir de uma fonte externa, como vCMS, obtenha o modo de sinalização que deve ser usado.
1. Crie os metadados relacionados à publicidade.
1. Se o comportamento padrão precisar ser substituído, especifique o `AdSignalingMode` usando `AdvertisingMetadata.setSignalingMode`.

   Os valores válidos são `DEFAULT, SERVER_MAP`, e `MANIFEST_CUES`.

   Você deve definir o modo de sinalização de anúncios antes de chamar `prepareToPlay`. Depois que o TVSDK começa a resolver e colocar anúncios na linha do tempo, as alterações no modo de sinalização de anúncios são ignoradas. Defina o modo ao criar a variável `AuditudeSettings` objeto.

1. Prossiga para a reprodução.

<!--<a id="example_3567B4A0D53E4DA99C10C13244454026"></a>-->
