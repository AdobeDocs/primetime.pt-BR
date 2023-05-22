---
description: O conteúdo de Full Event Replay (FER) é um stream ao vivo convertido em VOD ao adicionar a tag
title: Resolução e inserção do anúncio FER
exl-id: 9075932d-4e77-4249-af5d-0b392033907f
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---

# Resolução e inserção do anúncio FER{#fer-ad-resolving-and-insertion}

O conteúdo de Full Event Replay (FER) é um stream ao vivo convertido em VOD ao adicionar a tag #EXT-X-ENDLIST ao final do arquivo de manifesto. O fluxo retém os marcadores de sinalização de anúncio.

O TVSDK do navegador trata um fluxo de FER como VOD, portanto, por padrão, o modo de sinalização de anúncio é `SERVER_MAP`. No entanto, como o fluxo retém os marcadores de sinalização de anúncio, é possível definir o modo de sinalização de anúncio como `MANIFEST_CUES`, que permite usar os marcadores de sinalização de anúncio para inserção de anúncio.

Para ativar a inserção de anúncios usando marcadores de sinalização para um fluxo FER:

```js
var config = new AdobePSDK.MediaPlayerItemConfig(); 
config.adSignalingMode = AdobePSDK.AdSignalingMode.MANIFEST_CUES; 
player.replaceCurrentResource(mediaResource, config);
```

O comportamento de resolução e inserção de anúncios FER é semelhante à resolução e inserção de anúncios ao vivo. O TVSDK do navegador faz o seguinte:

1. Insere todos os anúncios precedentes no início do conteúdo.
1. Resolve anúncios especificados pelos pontos de sinalização definidos no manifesto.
1. Substitui partes do conteúdo principal por ad breaks com a mesma duração
1. Recalcula a linha de tempo virtual, se necessário.

**Restrição:** O TVSDK do navegador é compatível apenas com a reprodução de fluxos HLS FER. Além disso, os anúncios intermediários de MP4 não são compatíveis com os fluxos FER.
