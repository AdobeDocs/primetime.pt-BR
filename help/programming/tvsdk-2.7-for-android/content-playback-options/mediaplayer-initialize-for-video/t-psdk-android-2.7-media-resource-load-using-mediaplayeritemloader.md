---
description: Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem demora.
seo-description: Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem demora.
seo-title: Carregar um recurso de mídia usando MediaPlayerItemLoader
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
uuid: 43ca2470-1fd2-4f66-94fe-a12ed17b52d7
translation-type: tm+mt
source-git-commit: 21d1eae53cea303221de00765724e787cf6e84ef
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Carregue um recurso de mídia usando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem demora.

A classe `MediaPlayerItemLoader` ajuda a trocar um recurso de mídia pelo `MediaPlayerItem` atual sem anexar uma visualização a uma instância `MediaPlayer`, que alocaria recursos de hardware de decodificação de vídeo. Etapas adicionais são necessárias para o conteúdo protegido por DRM, mas este manual não as descreve.

>[!IMPORTANT]
>
>O TVSDK não suporta um único `QoSProvider` para trabalhar com `itemLoader` e `MediaPlayer`. Se seu aplicativo usar o Instant On, o aplicativo precisará manter duas `QoS` instâncias e gerenciar ambas para obter as informações. Consulte [instant-on](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) para obter mais informações.

1. Crie uma instância de `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
   
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
   
           public void onBufferingBegin() { 
               //Do something 
           } 
   
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       }); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   } 
   ```

   >[!TIP]
   >
   >Crie uma instância separada de `MediaPlayerItemLoader` para cada recurso. Não use uma instância `MediaPlayerItemLoader` para carregar vários recursos.

1. Implemente a classe `ItemLoaderListener` para receber notificações da instância `MediaPlayerItemLoader`.

   ```java
   private MediaPlayerItemLoader createLoader() { 
       MediaPlayerItemLoader itemLoader =   
         new MediaPlayerItemLoader(this, new MediaPlayerItemLoader.LoaderListener() { 
           public void onError(PSDKErrorCode mediaErrorCode, String description) { 
               //Do something 
           } 
           public void onLoadComplete(MediaPlayerItem playerItem) { 
               loader.prepareBuffer(); 
           } 
           public void onBufferingBegin() { 
               //Do something 
           } 
           public void onBufferPrepared() { 
               mPlayer.reset(); 
           }  
       } ); 
   
       itemLoader.setKeepRebufferingForLive(true); 
       return itemLoader; 
   }
   ```

   Na chamada de retorno `onLoadComplete()`, execute um dos seguintes procedimentos:

   * Certifique-se de que tudo o que possa afetar o buffering, por exemplo, selecionar WebVTT ou faixas de áudio, esteja completo e chame `prepareBuffer()` para aproveitar as vantagens do instantâneo.
   * Anexe o item à instância `MediaPlayer` usando `replaceCurrentItem()`.

   Se você chamar `prepareBuffer()`, você receberá o evento BUFFER_PREPARED em seu manipulador `onBufferPrepared` quando a preparação for concluída.

1. Chame `load` na instância `MediaPlayerItemLoader` e passe o recurso a ser carregado e, opcionalmente, a ID de conteúdo e uma instância `MediaPlayerItemConfig`.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para fazer o buffer a partir de um ponto diferente do início do fluxo, chame `prepareBuffer()` com a posição (em milissegundos) na qual o buffering do start será executado.
1. Use os métodos `replaceCurrentItem()` e `play()` de `MediaPlayer` para start a ser reproduzido a partir desse ponto.
1. Aguarde o status ocioso e chame `replaceCurrentItem`.
1. Toque o item.

   * Se o item for carregado, mas não armazenado em buffer:

      1. Aguarde o status inicializado.
      1. Chame `prepareToPlay()`.
      1. Aguarde o status PREPARADO.
      1. Chame `play()`.
   * Se o item estiver em buffer:

      1. Aguarde o evento preparado para buffer.
      1. Chame `play()`.