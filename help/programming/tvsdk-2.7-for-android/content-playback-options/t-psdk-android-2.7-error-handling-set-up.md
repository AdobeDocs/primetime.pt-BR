---
description: Você pode configurar um local para lidar com erros.
seo-description: Você pode configurar um local para lidar com erros.
seo-title: Configurar a manipulação de erros
title: Configurar a manipulação de erros
uuid: fde47fa5-5ca5-4be5-a7e7-3227c5e4c670
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef

---


# Configurar a manipulação de erros {#set-up-error-handling}

Você pode configurar um local para lidar com erros.

1. Implemente uma função de retorno de chamada de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   O TVSDK transmite informações do evento, como um `MediaPlayerStatusChangeEvent` objeto.
1. Na chamada de retorno, quando o status retornado for `MediaPlayerStatus.ERROR`, forneça lógica para tratar todos os erros.
1. Depois que o erro for tratado, redefina o `MediaPlayer` objeto ou carregue um novo recurso de mídia.

   Quando o `MediaPlayer` objeto está no status de erro, ele permanece nesse status até que você o redefina usando o `MediaPlayer.reset` método.

<!--<a id="example_E74BB605ED08450295B8902F1E4BB8F5"></a>-->

Por exemplo:

```java
mediaPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
        if (event.getStatus() == MediaPlayerStatus.ERROR) { 
        // handle TVSDK error here 
        } 
    } 
});
```

