---
description: No Adobe Primetime ad decisioning, é possível direcionar anúncios em pares de valores chave.
title: Informações de direcionamento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---

# Informações de direcionamento{#targeting-information}

No Adobe Primetime ad decisioning, é possível direcionar anúncios em pares de valores chave.

Para passar esses pares de valores principais para o TVSDK do navegador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```
