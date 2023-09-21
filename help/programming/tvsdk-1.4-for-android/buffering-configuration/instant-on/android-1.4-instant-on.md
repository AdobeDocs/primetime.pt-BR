---
description: O termo "instantâneo" refere-se ao pré-carregamento de um ou mais canais para que um usuário que seleciona um canal ou troca de canais veja o conteúdo reproduzido imediatamente. O buffering já estará concluído quando o usuário começar a assistir.
title: Instantâneo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Instantâneo {#instant-on}

O termo &quot;instantâneo&quot; refere-se ao pré-carregamento de um ou mais canais para que um usuário que seleciona um canal ou troca de canais veja o conteúdo reproduzido imediatamente. O buffering já estará concluído quando o usuário começar a assistir.

Sem ativação instantânea, o TVSDK inicializa a mídia a ser reproduzida, mas não inicia o buffering do fluxo até que o aplicativo chame `play`. O usuário não vê conteúdo até que o buffering seja concluído. Com o instant on, você pode iniciar várias instâncias do reprodutor de mídia (ou carregador de item do reprodutor de mídia), e o TVSDK inicia o buffering dos fluxos imediatamente.

Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamando `play` no novo canal inicia a reprodução imediatamente.

Embora não existam limites para o número de `MediaPlayer` instâncias que o TVSDK pode executar, executar mais instâncias consome mais recursos. O desempenho da aplicação pode ser afetado pelo número de instâncias em execução. Para obter mais informações sobre essas instâncias, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurar buffering para reprodução instantânea {#configure-buffering-for-instant-on-playback}

Com o instant on, os usuários podem alternar canais e a reprodução começa imediatamente, sem tempo de espera. Quando você ativa a ativação instantânea, o TVSDK armazena em buffer um ou mais canais antes do início da reprodução.

1. Confirme se o recurso foi carregado e está pronto para reprodução, verificando se o estado é PREPARADO.
1. Antes de chamar `play`, chamar `prepareBuffer` para cada `MediaPlayer` instância.

   Isso ativa a ativação instantânea, o que significa que o TVSDK inicia o buffering sem reproduzir o recurso de mídia. O TVSDK despacha a variável `BUFFERING_COMPLETED` evento quando o buffer estiver cheio.

   >[!NOTE]
   >
   >Por padrão, `prepareBuffer` e `prepareToPlay` configure o fluxo de mídia para começar a reproduzir a partir do início. Para começar em outra posição, passe a posição (em milissegundos) para `prepareToPlay`.

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

1. Ao receber a `BUFFERING_COMPLETE` evento, comece a reproduzir o item ou exiba feedback visual para indicar que o conteúdo está completamente em buffer.

   Se você chamar `play`, a reprodução deve começar imediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
