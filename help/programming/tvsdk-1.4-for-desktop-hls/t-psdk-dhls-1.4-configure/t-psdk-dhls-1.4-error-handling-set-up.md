---
description: Configure um único local para lidar com erros.
title: Configurar tratamento de erros
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '99'
ht-degree: 0%

---

# Configurar tratamento de erros{#set-up-error-handling}

Configure um único local para lidar com erros.

1. Implementar uma função de retorno de chamada de evento para `MediaPlayerStatusChangeEvent.STATUS_CHANGED`.

   O TVSDK transmite informações de eventos, como uma `MediaPlayerStatusChangeEvent` objeto.
1. Na chamada de retorno, quando o status do parâmetro do evento é `MediaPlayerStatus.ERROR`, fornecem lógica para lidar com todos os erros.
1. Após o tratamento do erro, redefina a `MediaPlayer` ou carregar um novo recurso de mídia.

   Quando a variável `MediaPlayer` objeto estiver no estado ERRO, ele não poderá sair desse estado até que você redefina o `MediaPlayer` objeto (por meio da variável `MediaPlayer.reset` ) ou carregar um novo recurso de mídia ( `MediaPlayer.replaceCurrentItem`).

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
