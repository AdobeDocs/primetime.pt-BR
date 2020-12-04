---
description: Configure um único local para lidar com erros.
seo-description: Configure um único local para lidar com erros.
seo-title: Configurar a manipulação de erros
title: Configurar a manipulação de erros
uuid: ff56180d-aa74-4b7c-a24c-e536d874c2e6
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 1%

---


# Configurar a manipulação de erros{#set-up-error-handling}

Configure um único local para lidar com erros.

1. Implemente uma função de retorno de chamada de evento para `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   O TVSDK transmite informações do evento, como um objeto `MediaPlayerStatusChangeEvent`.
1. Na chamada de retorno, quando o status do parâmetro do evento for `MediaPlayerStatus.ERROR`, forneça lógica para lidar com todos os erros.
1. Depois que o erro for tratado, redefina o objeto `MediaPlayer` ou carregue um novo recurso de mídia.

   Quando o objeto `MediaPlayer` estiver no estado ERROR, ele não poderá sair desse estado até que você redefina o objeto `MediaPlayer` (pelo método `MediaPlayer.reset`) ou carregue um novo recurso de mídia ( `MediaPlayer.replaceCurrentItem`).

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Por exemplo:

```
mediaPlayer.addEventListener(MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
                             onStatusChanged); 
 
private void onStatusChanged(event:MediaPlayerStatusChangeEvent):void { 
    if (event.status == MediaPlayerStatus.ERROR) { 
        var error:MediaError = event.error; 
        // handle TVSDK error here 
    } 
} 
```

