---
description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 1%

---


# Carregar um recurso de mídia usando MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.

Por meio da classe `MediaPlayerItemLoader`, é possível trocar um recurso de mídia pelo `MediaPlayerItem` correspondente sem anexar uma exibição a uma instância `MediaPlayer`, o que resultaria na alocação dos recursos de hardware de decodificação de vídeo. O processo de obter a instância `MediaPlayerItem` é assíncrono.

1. Implemente ouvintes de eventos para estes eventos `MediaPlayerItemLoader`:

   * `MediaPlayerItemLoaderEvent.ERROR` evento

      O TVSDK usa essa opção para informar ao aplicativo que ocorreu um erro. O TVSDK fornece uma propriedade de erro que contém informações de diagnóstico.

1. Registre esta instância no `MediaPlayerItemLoader`.
1. Chame `DefaultMediaPlayerItemLoader.load`, transmitindo uma instância de um objeto `MediaResource`.

   O URL do objeto `MediaResource` deve apontar para o fluxo para o qual você deseja obter informações. Por exemplo:

   ```
   private function onLoadError(event:MediaPlayerItemLoaderEvent):void { 
       // something went wrong - look at the error code and description 
       // contained within the event.error 
   } 
   private function onLoadCompleted(event:MediaPlayerItemLoaderEvent):void { 
       // information is available - look at the data in the "event.item" object 
   } 
   // instantiate the MediaPlayerItemLoader object and register event listeners 
   var itemLoader:MediaPlayerItemLoader = new DefaultMediaPlayerItemLoader(); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.ERROR, onLoadError); 
   itemLoader.addEventListener(MediaPlayerItemLoaderEvent.COMPLETED, onLoadCompleted); 
   // create the MediaResource instance and set the URL to point to the actual media stream 
   var mediaResource:MediaResource = 
     MediaResource.createFromURL("https://example.com/media/test_media.m3u8", null); 
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```

