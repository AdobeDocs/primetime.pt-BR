---
description: Ativar instantâneo em significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou alternam canais, o conteúdo é reproduzido imediatamente. O buffering é concluído até o momento em que o usuário começa a assistir.
title: Instantâneo
exl-id: a9c0b9d0-ef2b-4113-bd08-e2b2792b04fb
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Instantâneo {#instant-on}

Ativar instantâneo em significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou alternam canais, o conteúdo é reproduzido imediatamente. O buffering é concluído até o momento em que o usuário começa a assistir.

Sem o Instant On, o TVSDK inicializa a mídia a ser reproduzida, mas não inicia o buffering do fluxo até que o aplicativo chame `play`. O usuário não vê conteúdo até que o buffering seja concluído. Com o Instant On, é possível iniciar várias instâncias do reprodutor de mídia (ou carregador de item do reprodutor de mídia), e o TVSDK inicia o buffering dos fluxos imediatamente. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamando `play` no novo canal inicia a reprodução imediatamente.

Embora não existam limites para o número de `MediaPlayer` e `MediaPlayerItemLoader` instâncias que o TVSDK pode executar, executar mais instâncias consome mais recursos. O desempenho da aplicação pode ser afetado pelo número de instâncias que estão sendo executadas. Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia no reprodutor de mídia](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load.md).

>[!IMPORTANT]
>
>O TVSDK não oferece suporte a um único `QoSProvider` para trabalhar com ambos `itemLoader` e `MediaPlayer`. Se o cliente usar Ativação instantânea, o aplicativo precisará manter duas instâncias de QoS e gerenciar ambas para obter as informações.

Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md).

## Adicionar uma ocorrência de Provedor de QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Crie e anexe um provedor de QoS a um `mediaPlayerItemLoader` instância

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Quando a reprodução começar, use o `_qosProvider` para obter `timeToLoad` e `timeToPrepare` QoSdata. As métricas de QoS restantes podem ser recuperadas usando o `QoSProvider` anexado à `mediaPlayer`.

   Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-2.7-for-android/content-playback-options/mediaplayer-initialize-for-video/t-psdk-android-2.7-media-resource-load-using-mediaplayeritemloader.md#use-mediaplayeritemloader).

## Configurar buffering para Ativação Instantânea {#section_4FE346B7BE434BA8A2203896D6E52146}

O TVSDK fornece métodos e status para permitir usar o Instant On com um recurso de mídia.

>[!NOTE]
>
>O Adobe recomenda usar `MediaPlayerItemLoader` para InstantOn. Para usar `MediaPlayerItemLoader`, em vez de `MediaPlayer`, consulte media-resource-load-using-mediaplayeritemloader.

1. Confirme se o recurso foi carregado e se o reprodutor está preparado para reproduzir o recurso.
1. Antes de chamar `play`, chamar `prepareBuffer` para cada `MediaPlayer` instância.

   >[!NOTE]
   >
   >`prepareBuffer` ativa o Instant On e o TVSDK inicia o buffering imediatamente e envia o `BUFFERING_COMPLETED` evento quando o buffer estiver cheio.

   >[!TIP]
   >
   >Por padrão, `prepareBuffer` e `prepareToPlay` configure o fluxo de mídia para começar a reproduzir a partir do início. Para começar em outra posição, passe a posição (em milissegundos) para `prepareToPlay`.

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

1. Ao receber a `BUFFERING_COMPLETE` evento, comece a reproduzir o item ou exiba feedback visual para indicar que o conteúdo está completamente em buffer.

   >[!NOTE]
   >
   >Se você chamar `play`, a reprodução deve começar imediatamente.
