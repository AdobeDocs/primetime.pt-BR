---
description: É possível exibir legendas ao reproduzir conteúdo de vídeo.
seo-description: É possível exibir legendas ao reproduzir conteúdo de vídeo.
seo-title: Legendas
title: Legendas
uuid: 4dedcedc-50e5-4983-bb09-3f316337117e
translation-type: tm+mt
source-git-commit: 9c6a6f0b5ecff78796e37daf9d7bdb9fa686ee0c
workflow-type: tm+mt
source-wordcount: '64'
ht-degree: 3%

---


# Legendas{#captions}

É possível exibir legendas ao reproduzir conteúdo de vídeo.

Para manipular legendas, você deve adicionar o ouvinte do `AdobePSDK.PSDKEventType.CAPTIONS_UPDATED` evento:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.CAPTIONS_UPDATED,  
                        onCaptionsUpdateEvent); 
... 
function onCaptionsUpdateEvent (event) { 
  // code to show the captions icon and any settings button. 
<ph>
   For example: 
  var btnCC = document.getElementById("btn_captions"); 
   btnCC.classList.remove("invisible"); 
   
  var btnSettings = document.getElementById("btn_settings"); 
   btnSettings.classList.remove("invisible"); 
 } 
</ph>
```

A Estrutura da interface fornece uma implementação de comportamentos de legendas padrão, que pode ser modificada. Comportamentos de legendas ocultas também podem ser modificados estendendo os comportamentos de legendas fechadas padrão. Por exemplo:

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
