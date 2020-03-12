---
description: O termo instant on refere-se ao pré-carregamento de um ou mais canais para que o usuário que seleciona um canal ou canais de switching visualize o conteúdo sendo reproduzido imediatamente. O buffering já é feito quando o usuário começa a assistir.
seo-description: O termo instant on refere-se ao pré-carregamento de um ou mais canais para que o usuário que seleciona um canal ou canais de switching visualize o conteúdo sendo reproduzido imediatamente. O buffering já é feito quando o usuário começa a assistir.
seo-title: Instantâneo em
title: Instantâneo em
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Instantâneo em {#instant-on}

O termo instant on refere-se ao pré-carregamento de um ou mais canais para que o usuário que seleciona um canal ou canais de switching visualize o conteúdo sendo reproduzido imediatamente. O buffering já é feito quando o usuário começa a assistir.

Sem acionar instantaneamente, o TVSDK inicializa a mídia a ser reproduzida, mas não inicia o buffering do fluxo até que o aplicativo ligue `play`. O usuário não vê conteúdo até que o buffering seja concluído. Com o modo instantâneo ativado, você pode iniciar várias instâncias do player de mídia (ou carregador de item do player de mídia) e o TVSDK inicia o buffering dos fluxos imediatamente.

Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamar `play` o novo canal inicia a reprodução imediatamente.

Embora não haja limites para o número de `MediaPlayer` instâncias que o TVSDK pode executar, a execução de mais instâncias consome mais recursos. O desempenho do aplicativo pode ser afetado pelo número de instâncias em execução. Para obter mais informações sobre essas instâncias, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurar buffering para reprodução instantânea {#configure-buffering-for-instant-on-playback}

Com o modo instantâneo ligado, os usuários podem trocar de canal e a reprodução é iniciada imediatamente sem tempo de espera. Quando você ativa instantaneamente, o TVSDK armazena um ou mais canais em buffer antes do início da reprodução.

1. Confirme se o recurso foi carregado e está pronto para ser reproduzido verificando se o estado é PREPARADO.
1. Antes de chamar `play`, chame `prepareBuffer` para cada `MediaPlayer` instância.

   Isso ativa a ativação imediata, o que significa que o TVSDK inicia o buffering sem reproduzir o recurso de mídia. O TVSDK despacha o `BUFFERING_COMPLETED` evento quando o buffer está cheio.

   >[!NOTE]
   >
   >Por padrão, `prepareBuffer` e `prepareToPlay` configure o fluxo de mídia para iniciar a reprodução do início. Para começar em outra posição, coloque a posição (em milissegundos) em `prepareToPlay`.

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

1. Ao receber o `BUFFERING_COMPLETE` evento, comece a reproduzir o item ou exiba o feedback visual para indicar que o conteúdo está completamente armazenado em buffer.

   Se você ligar `play`, a reprodução deve começar imediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
