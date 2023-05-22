---
description: Você pode configurar um local no aplicativo para executar o tratamento de erros em resposta ao estado ERROR.
title: Configurar tratamento de erros
exl-id: c0ce1d80-85d5-4344-9ab0-bd56906421cb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Configurar tratamento de erros{#set-up-error-handling}

Você pode configurar um local no aplicativo para executar o tratamento de erros em resposta ao estado ERROR.

1. Adicionar um ouvinte de eventos para `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Por exemplo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. No ouvinte de eventos, quando a variável `event.status` é `AdobePSDK.MediaPlayerStatus.ERROR`, fornecem a lógica para lidar com todos os erros.
1. Após o tratamento do erro, redefina a `MediaPlayer` ou carregar um novo recurso de mídia.

       Quando o objeto MediaPlayer está no estado ERROR, ele não pode sair desse estado até que você conclua uma das seguintes tarefas:
   
   * Redefina o objeto MediaPlayer usando o `MediaPlayer.reset` método.
   * Carregar um novo recurso de mídia usando o `MediaPlayer.replaceCurrentResource` método.

<!--<a id="example_342CA5A8CD7C45BD88233C5BDBB17220"></a>-->

Por exemplo:

```js
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
onStatusChange = function (event) { 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.ERROR: 
            //handle error 
            break; 
    } 
} 
```
