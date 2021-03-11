---
description: O termo instantâneo em refere-se ao pré-carregamento de um ou mais canais, para que um usuário que seleciona um canal ou canais de switching visualize a reprodução do conteúdo imediatamente. O buffering já é feito até o momento em que o usuário começa a assistir.
title: Instantâneo em
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Instantâneo em {#instant-on}

O termo instantâneo em refere-se ao pré-carregamento de um ou mais canais, para que um usuário que seleciona um canal ou canais de switching visualize a reprodução do conteúdo imediatamente. O buffering já é feito até o momento em que o usuário começa a assistir.

Sem ativação imediata, o TVSDK inicializa a mídia a ser reproduzida, mas não inicia o buffering do fluxo até que o aplicativo chame `play`. O usuário não vê conteúdo até que o buffering seja concluído. Com o instantâneo ativado, você pode iniciar várias instâncias do reprodutor de mídia (ou carregador de item do reprodutor de mídia) e o TVSDK inicia o buffering dos fluxos imediatamente.

Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamar `play` no novo canal inicia a reprodução imediatamente.

Embora não haja limites para o número de instâncias `MediaPlayer` que o TVSDK pode executar, a execução de mais instâncias consome mais recursos. O desempenho do aplicativo pode ser afetado pelo número de instâncias em execução. Para obter mais informações sobre essas instâncias, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurar buffering para reprodução instantânea {#configure-buffering-for-instant-on-playback}

Com o instantâneo ativado, os usuários podem trocar de canal e a reprodução começa imediatamente sem o tempo de espera. Ao ativar o instantâneo, o TVSDK armazena um ou mais canais antes do início da reprodução.

1. Confirme se o recurso foi carregado e está pronto para ser reproduzido verificando se o estado é PREPARED.
1. Antes de chamar `play`, chame `prepareBuffer` para cada instância `MediaPlayer`.

   Isso ativa o instantâneo, o que significa que o TVSDK inicia o buffering sem reproduzir o recurso de mídia. O TVSDK despacha o evento `BUFFERING_COMPLETED` quando o buffer está cheio.

   >[!NOTE]
   >
   >Por padrão, `prepareBuffer` e `prepareToPlay` configuram o fluxo de mídia para iniciar a reprodução a partir do início. Para iniciar em outra posição, passe a posição (em milissegundos) para `prepareToPlay`.

   ```java
   @Override 
   public void onStateChanged(MediaPlayer.PlayerState state,  
                              MediaPlayerNotification notification) { 
       switch (state) { 
           case INITIALIZED: 
               // By default, prepareToPlay and prepareBuffer buffer and start playing 
               // from the beginning of the stream. To start at another position, 
               // pass it into prepareToPlay. This example starts 5 seconds into the stream. 
               _mediaPlayer.prepareToPlay(5000); 
               break; 
           case PREPARING: 
               break; 
           case PREPARED: 
               _mediaPlayer.prepareBuffer(); 
               break; 
           ... 
       } 
   }
   ```

1. Ao receber o evento `BUFFERING_COMPLETE`, comece a reproduzir o item ou exiba um feedback visual para indicar que o conteúdo está completamente armazenado em buffer.

   Se você chamar `play`, a reprodução deverá começar imediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
