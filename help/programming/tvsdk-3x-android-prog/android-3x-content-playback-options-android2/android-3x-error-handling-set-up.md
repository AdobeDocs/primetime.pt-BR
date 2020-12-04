---
description: Você pode configurar um local para lidar com erros.
seo-description: Você pode configurar um local para lidar com erros.
seo-title: Configurar a manipulação de erros
title: Configurar a manipulação de erros
uuid: 7c122830-6259-4e95-882e-fb1700454e6e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 1%

---


# Configurar a manipulação de erros {#set-up-error-handling}

Você pode configurar um local para lidar com erros.

1. Implemente uma função de retorno de chamada de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   O TVSDK transmite informações do evento, como um objeto `MediaPlayerStatusChangeEvent`.
1. Na chamada de retorno, quando o status retornado for `MediaPlayerStatus.ERROR`, forneça a lógica para tratar todos os erros.
1. Depois que o erro for tratado, redefina o objeto `MediaPlayer` ou carregue um novo recurso de mídia.

   Quando o objeto `MediaPlayer` estiver no status de erro, ele permanecerá nesse status até que você o redefina usando o método `MediaPlayer.reset`.

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
