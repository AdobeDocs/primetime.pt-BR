---
description: O TVSDK despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.
title: Ordem dos eventos de reprodução
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 0%

---

# Ordem dos eventos de reprodução{#order-of-playback-events}

O TVSDK despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.

<!--<a id="section_6E34A6C7936245D88DEB3315DA64598B"></a>-->

Os exemplos a seguir mostram a ordem de alguns eventos que incluem eventos de reprodução.

* Ao carregar um recurso de mídia com êxito por meio do `MediaPlayer.replaceCurrentResource`, a ordem dos eventos é:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` com status `MediaPlayerStatus.INITIALIZING`

   * `MediaPlayerItemEvent.ITEM_CREATED`
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` com status `MediaPlayerStatus.INITIALIZED`

* Ao se preparar para a reprodução por meio do `MediaPlayer.prepareToPlay`, a ordem dos eventos é:

   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` com status `MediaPlayerStatus.PREPARING`

   * `TimelineEvent.TIMELINE_UPDATED` se anúncios foram inseridos
   * `MediaPlayerStatusChangeEvent.STATUS_CHANGED` com status `MediaPlayerStatus.PREPARED`

* Para fluxos ao vivo/lineares, durante a reprodução, à medida que a janela de reprodução avança e as oportunidades adicionais são resolvidas, a ordem dos eventos é:

   * `MediaPlayerItemEvent.ITEM_UPDATED`
   * `TimelineEvent.TIMELINE_UPDATED` se anúncios foram inseridos

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

O exemplo a seguir mostra uma progressão típica de eventos:

```
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
public function onItemCreated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
public function onItemUpdated(event:MediaPlayerItemEvent):void { 
    var item:MediaPlayerItem = event.item; 
    ... 
} 
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
public function onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    switch(event.status){ 
        case MediaPlayerStatus.INITIALIZING: 
        case MediaPlayerStatus.INITIALIZED: 
        ... 
    } 
    ... 
} 
mediaPlayer.addEventListener(TimeChangeEvent.TIME_CHANGED, onTimeChanged); 
public function onTimeChanged(event:TimeChangeEvent):void { 
    var timeInMilliseconds:Number = event.time; 
    ... 
}
```
