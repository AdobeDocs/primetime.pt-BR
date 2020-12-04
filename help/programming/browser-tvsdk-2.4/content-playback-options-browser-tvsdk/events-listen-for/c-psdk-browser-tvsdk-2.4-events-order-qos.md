---
description: O TVSDK do navegador despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffering e busca.
seo-description: O TVSDK do navegador despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffering e busca.
seo-title: Eventos de QoS
title: Eventos de QoS
uuid: 3384bc51-b435-4cd9-a1f8-9abf2605205b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 1%

---


# Eventos QoS{#qos-events}

O TVSDK do navegador despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffering e busca.

Para ser notificado sobre todos os eventos relacionados a QoS, crie uma instância de `AdobePSDK.QOSProvider` e anexe a instância MediaPlayer a esta instância `QOSProvider`:

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

