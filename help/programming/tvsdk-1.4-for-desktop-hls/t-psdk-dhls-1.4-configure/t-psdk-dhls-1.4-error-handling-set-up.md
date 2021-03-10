---
description: Configure um único local para lidar com erros.
title: Configurar tratamento de erros
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 2%

---


# Configurar tratamento de erros{#set-up-error-handling}

Configure um único local para lidar com erros.

1. Implemente uma função de retorno de chamada de evento para `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   O TVSDK transmite informações do evento, como um objeto `MediaPlayerStatusChangeEvent` .
1. Na chamada de retorno, quando o status do parâmetro de evento for `MediaPlayerStatus.ERROR`, forneça a lógica para lidar com todos os erros.
1. Depois que o erro for tratado, redefina o objeto `MediaPlayer` ou carregue um novo recurso de mídia.

   Quando o objeto `MediaPlayer` está no estado ERROR, ele não poderá sair desse estado até que você redefina o objeto `MediaPlayer` (por meio do método `MediaPlayer.reset`) ou carregue um novo recurso de mídia ( `MediaPlayer.replaceCurrentItem`).

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

