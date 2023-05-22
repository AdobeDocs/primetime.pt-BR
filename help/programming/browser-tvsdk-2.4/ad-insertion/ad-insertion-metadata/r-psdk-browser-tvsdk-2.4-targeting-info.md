---
description: No Adobe Primetime ad decisioning, é possível direcionar anúncios em pares de valores chave.
title: Informações de direcionamento
exl-id: 25610f7d-6b14-4ed1-b61c-9e6bf13ba8e6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
