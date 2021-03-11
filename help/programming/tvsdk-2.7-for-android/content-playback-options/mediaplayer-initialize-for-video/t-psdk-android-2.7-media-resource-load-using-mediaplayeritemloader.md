---
description: O uso de MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é útil principalmente em fluxos pré-buffering, para que a reprodução possa começar sem atraso.
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Carregar um recurso de mídia usando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

O uso de MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é útil principalmente em fluxos pré-buffering, para que a reprodução possa começar sem atraso.

A classe `MediaPlayerItemLoader` ajuda a trocar um recurso de mídia pelo `MediaPlayerItem` atual sem anexar uma exibição a uma instância `MediaPlayer`, que alocaria recursos de hardware de decodificação de vídeo. Etapas adicionais são necessárias para conteúdo protegido por DRM, mas este manual não as descreve.

>[!IMPORTANT]
>
>O TVSDK não oferece suporte a um único `QoSProvider` para funcionar com `itemLoader` e `MediaPlayer`. Se o aplicativo usar o Instant On, o aplicativo precisará manter duas instâncias `QoS` e gerenciar ambas as instâncias para as informações. Consulte [instant-on](../../content-playback-options/buffering-configuration/c-psdk-android-2.7-instant-on.md) para obter mais informações.

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

   Na chamada de retorno `onLoadComplete()`, siga um destes procedimentos:

   * Certifique-se de que qualquer coisa que possa afetar o buffering, por exemplo, selecionar a WebVTT ou as faixas de áudio, esteja completo e chame `prepareBuffer()` para aproveitar as vantagens instantâneas.
   * Anexe o item à instância `MediaPlayer` usando `replaceCurrentItem()`.

   Se você chamar `prepareBuffer()`, você receberá o evento BUFFER_PREPARED em seu manipulador `onBufferPrepared` quando a preparação for concluída.

1. Chame `load` na instância `MediaPlayerItemLoader` e passe o recurso a ser carregado, além de uma ID de conteúdo e uma instância `MediaPlayerItemConfig` opcionalmente.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para fazer o buffer a partir de um ponto diferente do início do fluxo, chame `prepareBuffer()` com a posição (em milissegundos) em que o buffering será iniciado.
1. Use os métodos `replaceCurrentItem()` e `play()` de `MediaPlayer` para começar a reproduzir a partir desse ponto.
1. Aguarde o status de inatividade e chame `replaceCurrentItem`.
1. Reproduzir o item.

   * Se o item for carregado, mas não armazenado em buffer:

      1. Aguarde o status inicializado.
      1. Chame `prepareToPlay()`.
      1. Aguarde o status PREPARED.
      1. Chame `play()`.
   * Se o item estiver em buffer:

      1. Aguarde o evento preparado para buffer.
      1. Chame `play()`.