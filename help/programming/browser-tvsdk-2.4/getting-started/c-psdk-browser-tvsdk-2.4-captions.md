---
description: É possível exibir legendas ao reproduzir conteúdo de vídeo.
title: Legendas
exl-id: 2144a6b2-0b9a-49ea-ad44-997adf36cbe6
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '55'
ht-degree: 0%

---

# Legendas{#captions}

É possível exibir legendas ao reproduzir conteúdo de vídeo.

Para lidar com legendas, é necessário adicionar o `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` ouvinte de eventos:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.CAPTIONS_UPDATED,  
                        onCaptionsUpdateEvent); 
... 
function onCaptionsUpdateEvent (event) { 
  // code to show the captions icon and any settings button. 
<pre>
   For example: 
  var btnCC = document.getElementById("btn_captions"); 
   btnCC.classList.remove("invisible"); 
   
  var btnSettings = document.getElementById("btn_settings"); 
   btnSettings.classList.remove("invisible"); 
 } 
</pre>
```

A Estrutura da interface do usuário fornece uma implementação de comportamentos de legendas padrão, que podem ser modificadas. Comportamentos de legendas ocultas também podem ser modificados ao estender comportamentos padrão de legendas ocultas. Por exemplo:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer(‘.videoDiv', { 
player:{ 
    mediaResource: 'Specify Resource URL', 
    ccStyle: { 
    font:AdobePSDK.TextFormat.CURSIVE, 
    fontColor:AdobePSDK.TextFormat.BRIGHT_WHITE, 
    edgeColor:AdobePSDK.TextFormat.BLUE, 
    backgroundColor:AdobePSDK.TextFormat.BLACK, 
    fillColor:AdobePSDK.TextFormat.BLUE, 
    size:AdobePSDK.TextFormat.MEDIUM, 
    fontOpacity:100, 
    backgroundOpacity:1, 
    fillOpacity:1 
   } 
 } 
 
}); 
```
