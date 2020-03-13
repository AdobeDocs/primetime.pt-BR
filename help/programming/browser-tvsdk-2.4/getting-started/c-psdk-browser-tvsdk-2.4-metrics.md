---
description: O TVSDK do navegador fornece métricas para usar na análise e depuração. Você pode obter essas métricas usando o QoSProvider.
seo-description: O TVSDK do navegador fornece métricas para usar na análise e depuração. Você pode obter essas métricas usando o QoSProvider.
seo-title: Métricas
title: Métricas
uuid: 4734e532-1f83-4691-b1bd-785f78e55d8d
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Métricas{#metrics}

O TVSDK do navegador fornece métricas para usar na análise e depuração. Você pode obter essas métricas usando o QoSProvider.

Por exemplo:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

