---
description: Você pode configurar visuais para notificar o usuário de que o conteúdo está sendo armazenado em buffer.
title: Buffering
exl-id: 1b2f32b4-1839-4256-82d6-b262569aa751
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Buffering{#buffering}

Você pode configurar visuais para notificar o usuário de que o conteúdo está sendo armazenado em buffer.

Ouvir `AdobePSDK.PSDKEventType.BUFFERING_BEGIN` e `AdobePSDK.PSDKEventType.BUFFERING_END` eventos. Por exemplo:

```js
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_BEGIN,  
                        function (event) { 
                            buffering = true; 
                            // add buffering layer 
                        }); 
  
player.addEventListener(AdobePSDK.PSDKEventType.BUFFERING_END,  
                        function (event) { 
                           buffering = false; 
                           // remove buffering layer 
                        });
```

A Estrutura da interface do usuário fornece implementação de comportamento de sobreposição de buffering padrão, que pode ser estendido conforme mostrado abaixo:

```js
// Using UI Framework 
function myBufferingOverlayBehavior (element, configuration, player, localize, baseLog) { 
    return ptp.bufferingOverlayBehavior(element, configuration, player, localize, baseLog); 
} 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource:'Specify Resource URL', 
        bufferingOverlay: { 
            behavior: myBufferingOverlayBehavior, 
            classNames: 'ptp-buffering-overlay my_buffering_overlay_bar' 
        } 
    } 
 
}); 
```

Esta é a aparência do DOM resultante:

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```
