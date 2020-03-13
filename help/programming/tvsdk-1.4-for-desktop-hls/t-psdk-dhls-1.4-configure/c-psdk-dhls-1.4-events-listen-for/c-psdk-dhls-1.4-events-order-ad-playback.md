---
description: Quando a reprodução inclui publicidade, o TVSDK envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.
seo-description: Quando a reprodução inclui publicidade, o TVSDK envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.
seo-title: Ordem dos eventos publicitários
title: Ordem dos eventos publicitários
uuid: 34a6a606-2f2e-42de-88fd-c91202cafddf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ordem dos eventos publicitários{#order-of-advertising-events}

Quando a reprodução inclui publicidade, o TVSDK envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.

<!--<a id="section_69E3CCBC57BB48399799876E83908348"></a>-->

Ao reproduzir publicidades, a ordem dos eventos é:

* `AdBreakPlaybackEvent.AD_BREAK_STARTED`
* Os seguintes anúncios são enviados para cada anúncio no intervalo de anúncios:

   * `AdPlaybackEvent.AD_STARTED`
   * `AdPlaybackEvent.AD_PROGRESS` (várias vezes durante a reprodução de um anúncio)
   * `AdClickEvent.AD_CLICK` (para cada clique)
   * `AdPlaybackEvent.AD_COMPLETED`

* `AdBreakPlaybackEvent.AD_BREAK_COMPLETED`

O exemplo a seguir mostra uma progressão típica dos eventos de reprodução de anúncio:

```
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_STARTED, onAdBreakStarted); 
private function onAdBreakStarted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdBreakPlaybackEvent.AD_BREAK_COMPLETED, onAdBreakCompleted); 
private function onAdBreakCompleted(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
private function onAdStarted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_PROGRESS, onAdProgress); 
private function onAdProgress(event:AdBreakPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad;  
    var progress:uint = event.progress; 
    ... 
} 
mediaPlayer.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
private function onAdCompleted(event:AdPlaybackEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    ... 
} 
mediaPlayer.addEventListener(AdClickEvent.AD_CLICK, onAdClick); 
private function onAdClick(event:AdClickThroughEvent):void { 
    var adBreak:AdBreak = event.adBreak; 
    var ad:Ad = event.ad; 
    var info:AdClick = event.adClick; 
    ... 
} 
```

