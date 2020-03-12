---
description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
seo-description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
seo-title: Carregar um recurso de mídia usando MediaPlayerItemLoader
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
uuid: a7ec8f58-7357-4757-a402-e879dd6caec8
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Carregar um recurso de mídia usando MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.

Por meio da `MediaPlayerItemLoader` classe, é possível trocar um recurso de mídia pelo correspondente `MediaPlayerItem` sem anexar uma exibição a uma `MediaPlayer` instância, o que resultaria na alocação dos recursos de hardware de decodificação de vídeo. O processo de obtenção da `MediaPlayerItem` instância é assíncrono.

1. Implemente ouvintes de eventos para estes `MediaPlayerItemLoader` eventos:

   * `MediaPlayerItemLoaderEvent.ERROR` event

      O TVSDK usa isso para informar ao aplicativo que ocorreu um erro. O TVSDK fornece uma propriedade de erro que contém informações de diagnóstico.

1. Registre esta instância no `MediaPlayerItemLoader`.
1. Chamada `DefaultMediaPlayerItemLoader.load`, transmitindo uma instância de um `MediaResource` objeto.

   O URL do `MediaResource` objeto deve apontar para o fluxo para o qual você deseja obter informações. Por exemplo:

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

