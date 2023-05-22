---
description: Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma ocorrência de MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem atraso.
title: Carregar um recurso de mídia usando MediaPlayerItemLoader
exl-id: de61ec1c-f578-4e19-a131-51f36169c7ed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---

# Carregar um recurso de mídia usando MediaPlayerItemLoader {#load-a-media-resource-using-mediaplayeritemloader}

Usar MediaPlayerItemLoader ajuda a obter informações sobre um fluxo de mídia sem instanciar uma ocorrência de MediaPlayer. Isso é especialmente útil em fluxos pré-buffering para que a reprodução possa começar sem atraso.

A variável `MediaPlayerItemLoader` ajuda você a trocar um recurso de mídia pela classe atual `MediaPlayerItem` sem anexar uma visualização a uma `MediaPlayer` instância, que alocaria recursos de hardware de decodificação de vídeo. Etapas adicionais são necessárias para conteúdo protegido por DRM, mas este manual não as descreve.

>[!IMPORTANT]
>
>O TVSDK não oferece suporte a um único `QoSProvider` para trabalhar com ambos `itemLoader` e `MediaPlayer`. Se o aplicativo usar Ativação instantânea, ele precisará manter duas `QoS` instâncias e gerenciar ambas as instâncias para obter as informações. Consulte [Instantâneo](../../android-3x-content-playback-options-android2/buffering-configuration/android-3x-instant-on.md) para obter mais informações.

1. Criar uma instância de `MediaPlayerItemLoader`.

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
   >Criar uma instância separada de `MediaPlayerItemLoader` para cada recurso. Não use um `MediaPlayerItemLoader` instância para carregar vários recursos.

1. Implementar o `ItemLoaderListener` classe para receber notificações do `MediaPlayerItemLoader` instância.

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

   No `onLoadComplete()` retorne a chamada, siga um destes procedimentos:

   * Certifique-se de que qualquer item que possa afetar o buffering, por exemplo, a seleção de WebVTT ou trilhas de áudio, esteja concluído e chame `prepareBuffer()` para aproveitar o instante on.
   * Anexar o item à `MediaPlayer` instância usando `replaceCurrentItem()`.
   Se você chamar `prepareBuffer()`, você receberá o evento BUFFER_PREPARED no `onBufferPrepared` manipulador quando a preparação for concluída.
1. Chame `load` no `MediaPlayerItemLoader` instância e transmita o recurso a ser carregado e, opcionalmente, a ID de conteúdo, e uma `MediaPlayerItemConfig` instância.

   ```java
   loader = createLoader(); 
   MediaResource res = new MediaResource(mVideoUrl, MediaResource.Type.HLS, metadata); 
   loader.load(res, 233, getConfig());
   ```

1. Para armazenar em buffer de um ponto diferente do início do fluxo, chame `prepareBuffer()` com a posição (em milissegundos) em que o buffering deve ser iniciado.
1. Use o `replaceCurrentItem()` e `play()` métodos de `MediaPlayer` para começar a reproduzir a partir desse ponto.
1. Aguardar o status ocioso e chamar `replaceCurrentItem`.
1. Reproduzir o item.

   * Se o item estiver carregado, mas não armazenado em buffer:

      1. Aguarde o status inicializado.
      1. Chame `prepareToPlay()`.
      1. Aguarde o status PREPARADO.
      1. Chame `play()`.
   * Se o item estiver em buffer:

      1. Aguarde o evento preparado para buffer.
      1. Chame `play()`.
