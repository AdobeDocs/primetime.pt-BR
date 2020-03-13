---
description: Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem demora.
seo-description: Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem demora.
seo-title: Carregar um recurso de mídia usando MediaPlayerItemLoader
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
uuid: 504063af-1dd4-4268-88e7-ad5a247fdff7
translation-type: tm+mt
source-git-commit: 3fdae2b6babb578d2cacff970fd9c7b53ad2c5dc

---


# Carregar um recurso de mídia usando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma instância do MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem demora.

A `MediaPlayerItemLoader` classe ajuda a trocar um recurso de mídia para o atual `MediaPlayerItem` sem anexar uma exibição a uma `MediaPlayer` instância, que alocaria recursos de hardware de decodificação de vídeo. Etapas adicionais são necessárias para o conteúdo protegido por DRM, mas este manual não as descreve.

>[!IMPORTANT]
>
>O TVSDK não oferece suporte `QoSProvider` a um único para trabalhar com ambos `itemLoader` e `MediaPlayer`. Se seu aplicativo usar o Instant On, o aplicativo precisará manter duas `QoS` instâncias e gerenciar ambas para obter as informações. Consulte [Instant-on](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) para obter mais informações.

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
   >Crie uma instância separada de `MediaPlayerItemLoader` para cada recurso. Não use uma `MediaPlayerItemLoader` instância para carregar vários recursos.

1. Implemente a `ItemLoaderListener` classe para receber notificações da `MediaPlayerItemLoader` instância.

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

   Na `onLoadComplete()` chamada de retorno, execute um dos procedimentos a seguir:

   * Certifique-se de que tudo o que possa afetar o buffering, por exemplo, selecionar WebVTT ou faixas de áudio, esteja completo e chame `prepareBuffer()` para aproveitar as vantagens de instantaneamente.
   * Anexe o item à `MediaPlayer` instância usando `replaceCurrentItem()`.
   Se você ligar `prepareBuffer()`, você receberá o evento BUFFER_PREPARED no seu `onBufferPrepared` manipulador quando a preparação for concluída.
1. Chame `load` a instância e passe o recurso a ser carregado, e opcionalmente a ID de conteúdo e uma `MediaPlayerItemLoader` `MediaPlayerItemConfig` instância.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para fazer o buffer a partir de um ponto diferente do início do fluxo, chame `prepareBuffer()` com a posição (em milissegundos) na qual o buffering deve ser iniciado.
1. Use os `replaceCurrentItem()` e `play()` métodos de `MediaPlayer` início da reprodução a partir desse ponto.
1. Aguarde o status ocioso e faça uma chamada `replaceCurrentItem`.
1. Toque o item.

   * Se o item for carregado, mas não armazenado em buffer:

      1. Aguarde o status inicializado.
      1. Ligue `prepareToPlay()`.
      1. Aguarde o status PREPARADO.
      1. Ligue `play()`.
   * Se o item estiver em buffer:

      1. Aguarde o evento preparado para buffer.
      1. Ligue `play()`.