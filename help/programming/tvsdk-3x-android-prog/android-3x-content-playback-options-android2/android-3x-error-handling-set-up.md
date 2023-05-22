---
description: Você pode configurar um local para lidar com erros.
title: Configurar tratamento de erros
exl-id: 9b83b47e-6d30-452b-87c3-1e3a139f2e69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Configurar tratamento de erros {#set-up-error-handling}

Você pode configurar um local para lidar com erros.

1. Implementar uma função de retorno de chamada de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   O TVSDK transmite informações de eventos, como uma `MediaPlayerStatusChangeEvent` objeto.
1. No retorno de chamada, quando o status retornado for `MediaPlayerStatus.ERROR`, fornecem lógica para lidar com todos os erros.
1. Após o tratamento do erro, redefina a `MediaPlayer` ou carregar um novo recurso de mídia.

   Quando a variável `MediaPlayer` objeto estiver no status de erro, ele permanecerá nesse status até que você o redefina usando o `MediaPlayer.reset` método.

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
