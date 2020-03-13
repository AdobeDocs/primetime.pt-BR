---
description: O TVSDK do navegador despacha eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.
seo-description: O TVSDK do navegador despacha eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.
seo-title: Ordem dos eventos de reprodução
title: Ordem dos eventos de reprodução
uuid: 259a9a2d-3d28-4240-b392-cc81f5c3f0cf
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ordem dos eventos de reprodução{#order-of-playback-events}

O TVSDK do navegador despacha eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.

<!--<a id="section_D247A5873A854A079EFA6AC2E80AB894"></a>-->

Os exemplos a seguir mostram a ordem de alguns eventos que incluem eventos de reprodução.

* Ao carregar com êxito um recurso de mídia por meio `replaceCurrentResource`, a ordem dos eventos é:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` with `event.status =`

      * `MediaPlayerStatus.INITIALIZING`
      * `MediaPlayerStatus.INITIALIZED`

* Ao se preparar para a reprodução, `MediaPlayer.prepareToPlay`a ordem dos eventos é:

   * `AdobePSDK.MediaPlayerStatusChangeEvent` with `event.status =`

      * `MediaPlayerStatus.PREPARING`
      * `MediaPlayerStatus.PREPARED`

<!--<a id="section_76C13548AF934868B70757CA5489E516"></a>-->

O exemplo a seguir mostra uma progressão típica de eventos:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                 onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZING: 
            console.log("Player Status: INITIALIZING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
            console.log("Player Status: INITIALIZED"); 
            player.prepareToPlay(); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARING: 
            console.log("Player Status: PREPARING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PREPARED: 
            console.log("Player Status: PREPARED"); 
            if (autoPlay) { 
                player.play(); 
            } 
            else { 
                dispatchEvent(ReferencePlayer.Events.PreparedEvent,  
                              {target: this}); 
            } 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PLAYING: 
            console.log("Player Status: PLAYING"); 
            //update UI play/pause to show pause icon 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.PAUSED: 
            console.log("Player Status: PAUSED"); 
            //update UI play/pause to show play icon &  
            //display pause icon over video 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.SEEKING: 
            console.log("Player Status: SEEKING"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.COMPLETE: 
            console.log("Player Status: COMPLETE"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.RELEASED: 
            console.log("Player Status: RELEASED"); 
            break; 
 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            console.log("Player Status: ERROR"); 
            break; 
    } 
};
```

