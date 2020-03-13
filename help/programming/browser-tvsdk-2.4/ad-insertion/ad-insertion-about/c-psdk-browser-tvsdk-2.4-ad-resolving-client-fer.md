---
description: 'O conteúdo de Reprodução completa de eventos (FER) é um fluxo ao vivo convertido em VOD ao adicionar a tag #EXT-X-ENDLIST ao final do arquivo manifest. O fluxo mantém seus marcadores de sinalização de anúncios.'
seo-description: 'O conteúdo de Reprodução completa de eventos (FER) é um fluxo ao vivo convertido em VOD ao adicionar a tag #EXT-X-ENDLIST ao final do arquivo manifest. O fluxo mantém seus marcadores de sinalização de anúncios.'
seo-title: FER resolução e inserção de anúncios
title: FER resolução e inserção de anúncios
uuid: 85da0e92-17fe-4001-a53c-085dadd09756
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# FER resolução e inserção de anúncios{#fer-ad-resolving-and-insertion}

O conteúdo de Reprodução completa de eventos (FER) é um fluxo ao vivo convertido em VOD ao adicionar a tag #EXT-X-ENDLIST ao final do arquivo manifest. O fluxo mantém seus marcadores de sinalização de anúncios.

O TVSDK do navegador trata um fluxo FER como VOD, portanto, por padrão, o modo de sinalização do anúncio é `SERVER_MAP`. Entretanto, como o fluxo mantém seus marcadores de sinalização de anúncios, é possível definir o modo de sinalização de anúncios como `MANIFEST_CUES`, o que permite usar os marcadores de sinalização de anúncios para inserção de anúncios.

Para ativar a inserção de publicidade usando marcadores de sinalização para um fluxo FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

O comportamento de inserção e resolução de anúncios de FER é semelhante à resolução e inserção de anúncios em tempo real. O TVSDK do navegador faz o seguinte:

1. Insere todos os anúncios precedentes no início do conteúdo.
1. Resolve publicidades especificadas pelos pontos de sinalização definidos no manifesto.
1. Substitui partes do conteúdo principal por quebras de anúncios da mesma duração
1. Calcula novamente a linha do tempo virtual, se necessário.

**Restrição:** O TVSDK do navegador suporta apenas a reprodução de fluxos HLS FER. Além disso, os anúncios intermediários MP4 não são suportados com fluxos FER.
