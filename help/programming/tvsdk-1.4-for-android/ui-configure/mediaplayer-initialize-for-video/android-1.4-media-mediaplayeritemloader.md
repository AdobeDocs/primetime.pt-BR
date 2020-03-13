---
description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
seo-description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
seo-title: Carregar um recurso de mídia usando MediaPlayerItemLoader
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Carregar um recurso de mídia usando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.

Por meio da `MediaPlayerItemLoader` classe, é possível trocar um recurso de mídia pelo correspondente `MediaPlayerItem` sem anexar uma exibição a uma `MediaPlayer` instância, o que resultaria na alocação dos recursos de hardware de decodificação de vídeo. O processo de obtenção da `MediaPlayerItem` instância é assíncrono.

1. Implemente a interface `MediaPlayerItemLoader.LoaderListener` de retorno de chamada.

       Essa interface define dois métodos:
   
   * `LoaderListener.onError` função de retorno

      O TVSDK usa isso para informar ao aplicativo que ocorreu um erro. O TVSDK fornece um código de erro como parâmetros e uma string de descrição que contém informações de diagnóstico.

   * `LoaderListener.onError` função de retorno

      O TVSDK usa isso para informar ao aplicativo que as informações solicitadas estão disponíveis no formato de uma `MediaPlayerItem` instância transmitida como parâmetro para o retorno de chamada.

1. Registre essa instância no TVSDK transmitindo-a como um parâmetro para o construtor do `MediaPlayerItemLoader`.
1. Chamada `MediaPlayerItemLoader.load`, transmitindo uma instância de um `MediaResource` objeto.

   O URL do `MediaResource` objeto deve apontar para o fluxo para o qual você deseja obter informações. Por exemplo:

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

