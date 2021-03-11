---
description: O TVSDK do navegador fornece métricas para usar na análise e depuração. Você pode obter essas métricas usando o QoSProvider.
title: Métricas
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '40'
ht-degree: 5%

---


# Métricas{#metrics}

O TVSDK do navegador fornece métricas para usar na análise e depuração. Você pode obter essas métricas usando o QoSProvider.

Por exemplo:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
qosProvider.attachMediaPlayer(player); 
var metrics = qosProvider.playbackInformation;
```

