---
description: Você pode configurar um local no aplicativo para executar a manipulação de erros em resposta ao estado ERROR.
seo-description: Você pode configurar um local no aplicativo para executar a manipulação de erros em resposta ao estado ERROR.
seo-title: Configurar a manipulação de erros
title: Configurar a manipulação de erros
uuid: 9e650ea7-86cb-4489-a3fd-80cd2ccef41f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Configurar a manipulação de erros{#set-up-error-handling}

Você pode configurar um local no aplicativo para executar a manipulação de erros em resposta ao estado ERROR.

1. Adicione um ouvinte de evento para `AdobePSDK.MediaPlayerStatusChangeEvent`.

   Por exemplo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, 
                           onStatusChange);
   ```

1. Em seu ouvinte de eventos, quando o evento `event.status` for `AdobePSDK.MediaPlayerStatus.ERROR`, forneça a lógica para lidar com todos os erros.
1. Depois que o erro for tratado, redefina o `MediaPlayer` objeto ou carregue um novo recurso de mídia.

       Quando o objeto MediaPlayer estiver no estado ERROR, ele não poderá sair desse estado até que você conclua uma das seguintes tarefas:
   
   * Redefina o objeto MediaPlayer usando o `MediaPlayer.reset` método.
   * Carregue um novo recurso de mídia usando o `MediaPlayer.replaceCurrentResource` método.

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

