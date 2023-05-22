---
description: O TVSDK do navegador despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffering e busca.
title: Eventos de QoS
exl-id: b0fab68e-ef0f-4812-b4ad-3f69dcdf2d9e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---

# Eventos de QoS{#qos-events}

O TVSDK do navegador despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffering e busca.

Para ser notificado sobre todos os eventos relacionados à QoS, crie uma instância de `AdobePSDK.QOSProvider` e anexe a ocorrência de MediaPlayer a este `QOSProvider` instância:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configure um temporizador em seu aplicativo para verificar periodicamente o `playbackInformation` propriedade do `qosProvider` instância. A variável `playbackInformation` fornece um snapshot das estatísticas atuais de reprodução. Por exemplo:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```
