---
description: Configure um único local para lidar com erros.
title: Configurar tratamento de erros
exl-id: 2d0e0d08-d932-4b6e-8f95-494a2e666827
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Configurar tratamento de erros{#set-up-error-handling}

Configure um único local para lidar com erros.

1. Implementar uma função de retorno de chamada de evento para `MediaPlayerEvent.STATUS_CHANGED`.

   O TVSDK transmite informações de eventos, como uma `MediaPlayerStatusChangeEvent` objeto.
1. No retorno de chamada, quando o estado retornado for `MediaPlayerState.ERROR`, fornecem lógica para lidar com todos os erros.
1. Após o tratamento do erro, redefina a `MediaPlayer` ou carregar um novo recurso de mídia.

   Quando a variável `MediaPlayer` objeto estiver no estado de erro, ele permanecerá nesse estado até que você o redefina usando o `MediaPlayer.reset` método.

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
