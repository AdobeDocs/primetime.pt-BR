---
description: O TVSDK do navegador fornece métricas para usar na análise e depuração. Você pode obter essas métricas usando o QoSProvider.
title: Métricas
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 0%

---

# Métricas{#metrics}

O TVSDK do navegador fornece métricas para usar na análise e depuração. Você pode obter essas métricas usando o QoSProvider.

Por exemplo:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```
