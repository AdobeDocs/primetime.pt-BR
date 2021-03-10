---
description: O TVSDK do navegador despacha eventos de qualidade do serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffer e busca.
title: Eventos de QoS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 1%

---


# Eventos de QoS{#qos-events}

O TVSDK do navegador despacha eventos de qualidade do serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffer e busca.

Para ser notificado sobre todos os eventos relacionados a QoS, crie uma instância de `AdobePSDK.QOSProvider` e anexe a instância MediaPlayer a essa instância `QOSProvider`:

```js
var qosProvider = new AdobePSDK.QOSProvider(); 
// initialize QOS provider before setting media  
qosProvider.attachMediaPlayer(player);
```

Configure um temporizador no aplicativo para verificar periodicamente a propriedade `playbackInformation` da instância `qosProvider`. A propriedade `playbackInformation` fornece um instantâneo das estatísticas de reprodução atuais. Por exemplo:

```js
var startTimer = function () { 
   var metrics = qosProvider.playbackInformation; 
 
    //analyze metrics 
    //for e.g. metrics.timeToFirstByte ; metrics.timeToLoad etc.  
    //refer API doc for supported metrics  
} 
window.setTimeout(startTimer, 500) 
```

