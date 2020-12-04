---
description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
seo-description: Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.
seo-title: Carregar um recurso de mídia usando MediaPlayerItemLoader
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
uuid: b2311ddc-f059-4775-8553-fc354ec2636b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Carregue um recurso de mídia usando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Outra maneira de resolver um recurso de mídia é com MediaPlayerItemLoader. Isso é útil quando você deseja obter informações sobre um fluxo de mídia específico sem instanciar uma instância do MediaPlayer.

Por meio da classe `MediaPlayerItemLoader`, é possível trocar um recurso de mídia pelo `MediaPlayerItem` correspondente sem anexar uma visualização a uma instância `MediaPlayer`, o que resultaria na alocação dos recursos de hardware de decodificação de vídeo. O processo de obtenção da instância `MediaPlayerItem` é assíncrono.

1. Implemente a interface de retorno de chamada `MediaPlayerItemLoader.LoaderListener`.

       Essa interface define dois métodos:
   
   * `LoaderListener.onError` função de retorno

      O TVSDK usa isso para informar ao aplicativo que ocorreu um erro. O TVSDK fornece um código de erro como parâmetros e uma string de descrição que contém informações de diagnóstico.

   * `LoaderListener.onError` função de retorno

      O TVSDK usa isso para informar ao aplicativo que as informações solicitadas estão disponíveis na forma de uma instância `MediaPlayerItem` transmitida como parâmetro para o retorno de chamada.

1. Registre essa instância no TVSDK transmitindo-a como um parâmetro para o construtor do `MediaPlayerItemLoader`.
1. Chame `MediaPlayerItemLoader.load`, transmitindo uma instância de um objeto `MediaResource`.

   O URL do objeto `MediaResource` deve apontar para o fluxo para o qual você deseja obter informações. Por exemplo:

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

