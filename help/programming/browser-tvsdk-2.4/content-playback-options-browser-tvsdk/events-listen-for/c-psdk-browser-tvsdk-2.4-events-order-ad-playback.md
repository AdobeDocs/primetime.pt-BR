---
description: Quando a reprodução inclui publicidade, o TVSDK do navegador despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.
title: Ordem dos eventos de publicidade
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 0%

---

# Ordem dos eventos de publicidade{#order-of-advertising-events}

Quando a reprodução inclui publicidade, o TVSDK do navegador despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Ao reproduzir anúncios, a ordem dos eventos é:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* Os itens a seguir são despachados para cada anúncio no ad break:

   * `AdobePSDK.PSDKEventType.AD_STARTED`
   * `AdobePSDK.PSDKEventType.AD_PROGRESS` (várias vezes durante a reprodução de um anúncio)
   * `AdobePSDK.PSDKEventType.AD_COMPLETED`

* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`

O exemplo a seguir mostra uma progressão típica de eventos de reprodução de anúncio:

```js
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_STARTED, onAdbreakStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_PROGRESS, onAdProgress); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted); 
player.addEventListener(AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED, onAdbreakCompleted);
```
