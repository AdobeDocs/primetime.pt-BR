---
description: Habilitar instantaneamente significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou canais de switch, o conteúdo é reproduzido imediatamente. O buffering é concluído quando o usuário começa a assistir.
seo-description: Habilitar instantaneamente significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou canais de switch, o conteúdo é reproduzido imediatamente. O buffering é concluído quando o usuário começa a assistir.
seo-title: Instantâneo ativado
title: Instantâneo ativado
uuid: 5b1ceace-cae7-44c7-b4b9-d45078d58cc3
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Instantâneo ativado {#instant-on}

Habilitar instantaneamente significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou canais de switch, o conteúdo é reproduzido imediatamente. O buffering é concluído quando o usuário começa a assistir.

Sem ativação imediata, o TVSDK inicializa a mídia a ser reproduzida, mas não inicia o buffering do fluxo até que o aplicativo ligue `play`. O usuário não vê conteúdo até que o buffering seja concluído. Com o Instant On, você pode iniciar várias instâncias do media player (ou carregador de itens do media player) e o TVSDK inicia o buffering dos fluxos imediatamente. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamar `play` o novo canal inicia a reprodução imediatamente.

Embora não haja limites para o número de instâncias `MediaPlayer` e `MediaPlayerItemLoader` instâncias que o TVSDK pode executar, a execução de mais instâncias consome mais recursos. O desempenho do aplicativo pode ser afetado pelo número de instâncias em execução. Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia no player](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md)de mídia.

>[!IMPORTANT]
>
>O TVSDK não oferece suporte `QoSProvider` a um único para trabalhar com ambos `itemLoader` e `MediaPlayer`. Se o cliente usar o Instant On, o aplicativo precisará manter duas instâncias de QoS e gerenciar ambas as instâncias para obter as informações.

Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Adicionar uma instância do Provedor QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Criar e anexar um Provedor QoS a uma `mediaPlayerItemLoader` instância

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Depois que a reprodução começar, use o para obter `_qosProvider` e `timeToLoad` `timeToPrepare` QoSdata. As métricas de QoS restantes podem ser recuperadas usando o `QoSProvider` anexo ao `mediaPlayer`.

   Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurar buffering para Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

O TVSDK fornece métodos e status para permitir o uso do Instant On com um recurso de mídia.

>[!NOTE]
>
>A Adobe recomenda usar `MediaPlayerItemLoader` para o InstantOn. Para usar `MediaPlayerItemLoader`, em vez de `MediaPlayer`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Confirme se o recurso foi carregado e se o player está preparado para reproduzir o recurso.
1. Antes de chamar `play`, chame `prepareBuffer` para cada `MediaPlayer` instância.

   `prepareBuffer` ativa o Instant On e o TVSDK inicia o buffering imediatamente e despacha o `BUFFERING_COMPLETED` evento quando o buffer está cheio.

   >[!TIP]
   >
   >Por padrão, `prepareBuffer` e `prepareToPlay` configure o fluxo de mídia para iniciar a reprodução do início. Para iniciar em outra posição, passe a posição (em milissegundos) para `prepareToPlay`.

   ```
   @Override 
   public void onStatusChanged(MediaPlayerStatus status) { 
       switch (status) { 
           case INITIALIZED: 
               // This example starts 5 seconds into the stream. 
               mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. Ao receber o `BUFFERING_COMPLETE` evento, comece a reproduzir o item ou exiba o feedback visual para indicar que o conteúdo está completamente armazenado em buffer.

   >[!NOTE]
   >
   >Se você ligar `play`, a reprodução deve começar imediatamente.