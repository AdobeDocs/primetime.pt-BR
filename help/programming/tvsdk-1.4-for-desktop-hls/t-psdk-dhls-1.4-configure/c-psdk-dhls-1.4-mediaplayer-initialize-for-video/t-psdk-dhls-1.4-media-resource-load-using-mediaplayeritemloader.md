---
description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
exl-id: 08379bd8-1602-4013-a6fb-b1aa6ba539aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 0%

---

# Carregar um recurso de mídia usando MediaPlayerItemLoader{#load-a-media-resource-using-mediaplayeritemloader}

Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.

Por meio da `MediaPlayerItemLoader` classe, você pode trocar um recurso de mídia pela classe correspondente `MediaPlayerItem` sem anexar uma visualização a uma `MediaPlayer` que levaria à alocação dos recursos de hardware de decodificação de vídeo. O processo de obtenção da `MediaPlayerItem` é assíncrona.

1. Implementar ouvintes de eventos para esses `MediaPlayerItemLoader` eventos:

   * `MediaPlayerItemLoaderEvent.ERROR` evento

      O TVSDK usa isso para informar ao aplicativo que ocorreu um erro. O TVSDK fornece uma propriedade de erro que contém informações de diagnóstico.

1. Registre esta instância na `MediaPlayerItemLoader`.
1. Chame `DefaultMediaPlayerItemLoader.load`, transmitindo uma instância de um `MediaResource` objeto.

   O URL do `MediaResource` O objeto deve apontar para o fluxo para o qual você deseja obter informações. Por exemplo:

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
