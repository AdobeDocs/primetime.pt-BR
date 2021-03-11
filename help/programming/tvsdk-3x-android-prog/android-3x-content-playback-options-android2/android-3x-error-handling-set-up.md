---
description: Você pode configurar um local para lidar com erros.
title: Configurar tratamento de erros
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 2%

---


# Configurar o tratamento de erros {#set-up-error-handling}

Você pode configurar um local para lidar com erros.

1. Implemente uma função de retorno de chamada de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   O TVSDK transmite informações do evento, como um objeto `MediaPlayerStatusChangeEvent` .
1. Na chamada de retorno, quando o status retornado for `MediaPlayerStatus.ERROR`, forneça lógica para lidar com todos os erros.
1. Depois que o erro for tratado, redefina o objeto `MediaPlayer` ou carregue um novo recurso de mídia.

   Quando o objeto `MediaPlayer` está no status de erro, ele permanece nesse status até que você o redefina usando o método `MediaPlayer.reset`.

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
