---
description: 'O conteúdo de Reprodução completa de evento (FER) é um fluxo ao vivo convertido em VOD ao adicionar a tag #EXT-X-ENDLIST ao final do arquivo de manifesto. O fluxo retém seus marcadores de sinalização de anúncio.'
title: FER resolução e inserção de anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# FER resolução e inserção de anúncios{#fer-ad-resolving-and-insertion}

O conteúdo de Reprodução completa de evento (FER) é um fluxo ao vivo convertido em VOD ao adicionar a tag #EXT-X-ENDLIST ao final do arquivo de manifesto. O fluxo retém seus marcadores de sinalização de anúncio.

O TVSDK do navegador trata um fluxo FER como VOD, portanto, por padrão, o modo de sinalização de anúncio é `SERVER_MAP`. No entanto, como o fluxo retém seus marcadores de sinalização de anúncio, você pode definir o modo de sinalização de anúncio como `MANIFEST_CUES`, o que permite usar os marcadores de sinalização de anúncio para inserção de anúncio.

Para ativar a inserção de anúncio usando marcadores de sinalização para um fluxo FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

O comportamento de resolução e inserção de anúncios FER é semelhante à resolução e inserção de anúncios em tempo real. O TVSDK do navegador faz o seguinte:

1. Insere quaisquer anúncios precedentes no início do conteúdo.
1. Resolve as publicidades especificadas pelos pontos de sinalização definidos no manifesto.
1. Substitui partes do conteúdo principal por ad breaks da mesma duração
1. Calcula novamente a linha do tempo virtual, se necessário.

**Restrição:** o TVSDK do navegador suporta apenas a reprodução de fluxos de FER HLS. Além disso, os anúncios intermediários MP4 não são compatíveis com fluxos FER.
