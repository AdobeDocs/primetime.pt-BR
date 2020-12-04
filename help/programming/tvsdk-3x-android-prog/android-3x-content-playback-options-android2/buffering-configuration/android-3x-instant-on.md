---
description: Habilitar instantaneamente significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou alternam entre canais, o conteúdo é reproduzido imediatamente. O buffering é concluído quando o usuário start assistindo.
seo-description: Habilitar instantaneamente significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou alternam entre canais, o conteúdo é reproduzido imediatamente. O buffering é concluído quando o usuário start assistindo.
seo-title: Instantâneo ativado
title: Instantâneo ativado
uuid: 5b1ceace-cae7-44c7-b4b9-d45078d58cc3
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# Instantâneo em {#instant-on}

Habilitar instantaneamente significa que um ou mais canais são pré-carregados. Quando os usuários selecionam um canal ou alternam entre canais, o conteúdo é reproduzido imediatamente. O buffering é concluído quando o usuário start assistindo.

Sem o Instant On, o TVSDK inicializa a mídia a ser reproduzida, mas não faz o buffer do start do fluxo até que o aplicativo chame `play`. O usuário não vê conteúdo até que o buffering seja concluído. Com o Instant On, você pode iniciar várias instâncias do player de mídia (ou carregador de item do player de mídia) e start TVSDK para armazenar os fluxos imediatamente em buffer. Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamando `play` na reprodução dos novos start do canal imediatamente.

Embora não haja limites para o número de instâncias `MediaPlayer` e `MediaPlayerItemLoader` que o TVSDK pode executar, a execução de mais instâncias consome mais recursos. O desempenho do aplicativo pode ser afetado pelo número de instâncias em execução. Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia no media player](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-load.md).

>[!IMPORTANT]
>
>O TVSDK não suporta um único `QoSProvider` para trabalhar com `itemLoader` e `MediaPlayer`. Se o cliente usar o Instant On, o aplicativo precisará manter duas instâncias de QoS e gerenciar ambas as instâncias para obter as informações.

Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Adicionar uma instância do Provedor QoS a mediaPlayerItemLoader {#section_2F9F24C7BFAD49599D043D64F767F9A0}

* Criar e anexar um Provedor QoS a uma instância `mediaPlayerItemLoader`

   ```
   // Create an instance of QoSProvider  
   private QOSProvider _qosProvider = new QOSProvider(this._context);  
   
   // Attach the QoSProvider instance to the mediaPlayerItemLoaderInstance  
   // (before calling load API on mediaPlayerItemLoader instance)  
   _qosProvider.attachMediaPlayerItemLoader(this._loader); 
   ```

   Depois dos start de reprodução, use `_qosProvider` para obter `timeToLoad` e `timeToPrepare` QoSdata. As métricas de QoS restantes podem ser recuperadas usando o `QoSProvider` anexado ao `mediaPlayer`.

   Para obter mais informações sobre `MediaPlayerItemLoader`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

## Configurar buffering para Instant On {#section_4FE346B7BE434BA8A2203896D6E52146}

O TVSDK fornece métodos e status para permitir o uso do Instant On com um recurso de mídia.

>[!NOTE]
>
>O Adobe recomenda usar `MediaPlayerItemLoader` para InstantOn. Para usar `MediaPlayerItemLoader`, em vez de `MediaPlayer`, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/mediaplayer-initialize-for-video/android-3x-media-resource-mediaplayeritemloader.md).

1. Confirme se o recurso foi carregado e se o player está preparado para reproduzir o recurso.
1. Antes de chamar `play`, chame `prepareBuffer` para cada instância `MediaPlayer`.

   `prepareBuffer` habilita o buffer de start Instant On e TVSDK imediatamente e despacha o  `BUFFERING_COMPLETED` evento quando o buffer estiver cheio.

   >[!TIP]
   >
   >Por padrão, `prepareBuffer` e `prepareToPlay` configuram o fluxo de mídia para o start reproduzido desde o início. Para start em outra posição, passe a posição (em milissegundos) para `prepareToPlay`.

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

1. Quando você recebe o evento `BUFFERING_COMPLETE`, o start reproduz o item ou exibe o feedback visual para indicar que o conteúdo está completamente armazenado em buffer.

   >[!NOTE]
   >
   >Se você chamar `play`, a reprodução deve começar imediatamente.