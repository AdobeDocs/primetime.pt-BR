---
description: Na decisão do Adobe Primetime ad, você pode direcionar anúncios em pares de valor chave.
seo-description: Na decisão do Adobe Primetime ad, você pode direcionar anúncios em pares de valor chave.
seo-title: Informações de direcionamento
title: Informações de direcionamento
uuid: 72114bef-36a1-4f2d-92e8-59f4885d70d2
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Informações de direcionamento{#targeting-information}

Na decisão do Adobe Primetime ad, você pode direcionar anúncios em pares de valor chave.

Para passar estes pares de valores chave para o TVSDK do navegador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

