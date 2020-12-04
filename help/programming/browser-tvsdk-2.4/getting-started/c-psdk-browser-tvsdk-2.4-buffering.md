---
description: Você pode configurar visuais para notificar ao usuário que o conteúdo está sendo armazenado em buffer.
seo-description: Você pode configurar visuais para notificar ao usuário que o conteúdo está sendo armazenado em buffer.
seo-title: Buffering
title: Buffering
uuid: da9498ee-c736-4093-97a2-250d3ad56d49
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '69'
ht-degree: 2%

---


# Buffering{#buffering}

Você pode configurar visuais para notificar ao usuário que o conteúdo está sendo armazenado em buffer.

Analise os eventos `AdobePSDK.PSDKEventType.BUFFERING_BEGIN` e `AdobePSDK.PSDKEventType.BUFFERING_END`. Por exemplo:

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

A Estrutura da interface do usuário fornece a implementação padrão do comportamento de sobreposição de buffering, que pode ser estendida como mostrado abaixo:

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

Veja a aparência do DOM do resultado:

```
<div id=" videoDiv" class="ptp-root-element"> 
<div name="videoPlayer" value="videoPlayer" class="ptp-main-video-div-style"> 
<div name="bufferingOverlay" value="bufferingOverlay" class="ptp-buffering-overlay my_buffering_overlay_bar'"></div> 
</div> 
</div> 
```

