---
description: No Adobe Primetime ad decisioning, você pode direcionar anúncios em pares de valores chave.
title: Informações de direcionamento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '37'
ht-degree: 0%

---


# Informações de definição de metas{#targeting-information}

No Adobe Primetime ad decisioning, você pode direcionar anúncios em pares de valores chave.

Para transmitir esses pares de valores chave ao TVSDK do navegador:

```js
var auditudeSettings = new AdobePSDK.AuditudeSettings(); 
var targetingInfo = new AdobePSDK.Metadata(); 
 
// Add key value pairs to targetingInfo 
targetingInfo.setValue(key1, value1); 
targetingInfo.setValue(key2, value2); 
 
auditudeSettings.targetingInfo = targetingInfo;
```

