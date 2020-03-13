---
description: Quando a reprodução inclui publicidade, o TVSDK do navegador envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.
seo-description: Quando a reprodução inclui publicidade, o TVSDK do navegador envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.
seo-title: Ordem dos eventos publicitários
title: Ordem dos eventos publicitários
uuid: 9787e6ac-5e52-4d7d-8fc7-f7609633707c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ordem dos eventos publicitários{#order-of-advertising-events}

Quando a reprodução inclui publicidade, o TVSDK do navegador envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Ao reproduzir publicidades, a ordem dos eventos é:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* Os seguintes anúncios são enviados para cada anúncio no intervalo de anúncios:

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (várias vezes durante a reprodução de um anúncio)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

O exemplo a seguir mostra uma progressão típica dos eventos de reprodução de anúncio:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```

