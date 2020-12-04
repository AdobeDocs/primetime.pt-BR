---
description: Configure um único local para lidar com erros.
seo-description: Configure um único local para lidar com erros.
seo-title: Configurar a manipulação de erros
title: Configurar a manipulação de erros
uuid: a3182fce-85ac-4dad-bdb3-f9bfbdb2c62d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '100'
ht-degree: 2%

---


# Configurar a manipulação de erros{#set-up-error-handling}

Configure um único local para lidar com erros.

1. Implemente uma função de retorno de chamada de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   O TVSDK transmite informações do evento, como um objeto `MediaPlayerStatusChangeEvent`.
1. Na chamada de retorno, quando o estado retornado for `MediaPlayerState.ERROR`, forneça a lógica para tratar todos os erros.
1. Depois que o erro for tratado, redefina o objeto `MediaPlayer` ou carregue um novo recurso de mídia.

   Quando o objeto `MediaPlayer` estiver no estado de erro, ele permanecerá nesse estado até que você o redefina usando o método `MediaPlayer.reset`.

<!--<a id="example_49FF225E92EA494AA06B2E5F26101F4C"></a>-->

Por exemplo:

```java
mediaPlayer.addEventListener( 
  MediaPlayerEvent.STATUS_CHANGED, new StatusChangedEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
            // handle TVSDK error here 
        } 
    } 
});
```

