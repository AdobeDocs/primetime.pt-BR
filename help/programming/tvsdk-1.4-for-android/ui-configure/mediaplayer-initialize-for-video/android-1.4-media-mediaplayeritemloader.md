---
description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
exl-id: 9d129497-8a71-433a-a542-f49be519893b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 0%

---

# Carregar um recurso de mídia usando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.

Por meio da `MediaPlayerItemLoader` classe, você pode trocar um recurso de mídia pela classe correspondente `MediaPlayerItem` sem anexar uma visualização a uma `MediaPlayer` que levaria à alocação dos recursos de hardware de decodificação de vídeo. O processo de obtenção da `MediaPlayerItem` é assíncrona.

1. Implementar o `MediaPlayerItemLoader.LoaderListener` interface de retorno de chamada.

       Essa interface define dois métodos:
   
   * `LoaderListener.onError` função de retorno de chamada

      O TVSDK usa isso para informar ao aplicativo que ocorreu um erro. O TVSDK fornece um código de erro como parâmetros e uma string de descrição que contém informações de diagnóstico.

   * `LoaderListener.onError` função de retorno de chamada

      O TVSDK usa isso para informar ao aplicativo que as informações solicitadas estão disponíveis no formato de um `MediaPlayerItem` que é passada como parâmetro para o retorno de chamada.

1. Registre essa instância no TVSDK passando-a como um parâmetro para o construtor do `MediaPlayerItemLoader`.
1. Chame `MediaPlayerItemLoader.load`, transmitindo uma instância de um `MediaResource` objeto.

   O URL do `MediaResource` O objeto deve apontar para o fluxo para o qual você deseja obter informações. Por exemplo:

   ```java
   // instantiate the listener interface 
   MediaPlayerItemLoader.LoaderListener _itemLoaderListener = 
     new MediaPlayerItemLoader.LoaderListener() { 
       @Override 
       public void onError(MediaErrorCode mediaErrorCode, String description) { 
           // something went wrong - look at the error code and description 
       } 
       @Override 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
           // information is available - look at the data in the "playerItem" object 
       } 
   } 
   
   // instantiate the MediaPlayerItemLoader object (pass the listener as parameter) 
   MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(_itemLoaderListener); 
   
   // create the MediaResource instance and set the URL to point to the actual media stream 
   MediaResource mediaResource =  
     MediaResource.createFromUrl("https://test.com/test_media.m3u8", null); 
   
   // load the media resource 
   itemLoader.load(mediaResource); 
   ```
