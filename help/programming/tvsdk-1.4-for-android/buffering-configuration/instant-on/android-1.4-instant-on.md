---
description: O termo instant on refere-se ao pré-carregamento de um ou mais canais para que o usuário que seleciona um canal ou comuta canais visualize a reprodução imediata do conteúdo. O buffering já é feito quando o usuário start assistindo.
seo-description: O termo instant on refere-se ao pré-carregamento de um ou mais canais para que o usuário que seleciona um canal ou comuta canais visualize a reprodução imediata do conteúdo. O buffering já é feito quando o usuário start assistindo.
seo-title: Instantâneo em
title: Instantâneo em
uuid: 4cb4d221-170f-46e8-af26-32f259377617
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 0%

---


# Instantâneo em {#instant-on}

O termo instant on refere-se ao pré-carregamento de um ou mais canais para que o usuário que seleciona um canal ou comuta canais visualize a reprodução imediata do conteúdo. O buffering já é feito quando o usuário start assistindo.

Sem acionar instantaneamente, o TVSDK inicializa a mídia a ser reproduzida, mas não faz o buffer do start do fluxo até que o aplicativo chame `play`. O usuário não vê conteúdo até que o buffering seja concluído. Com o modo instantâneo ativado, você pode iniciar várias instâncias do player de mídia (ou carregador de item do player de mídia) e start TVSDK que fazem buffering nos fluxos imediatamente.

Quando um usuário altera o canal e o fluxo é armazenado em buffer corretamente, chamando `play` na reprodução dos novos start do canal imediatamente.

Embora não haja limites para o número de instâncias `MediaPlayer` que o TVSDK pode executar, a execução de mais instâncias consome mais recursos. O desempenho do aplicativo pode ser afetado pelo número de instâncias em execução. Para obter mais informações sobre essas instâncias, consulte [Carregar um recurso de mídia usando MediaPlayerItemLoader](../../../tvsdk-1.4-for-android/ui-configure/mediaplayer-initialize-for-video/android-1.4-media-mediaplayeritemloader.md).

## Configurar buffering para reprodução instantânea {#configure-buffering-for-instant-on-playback}

Com o modo instantâneo ligado, os usuários podem alternar os canais e os start de reprodução imediatamente sem tempo de espera. Quando você ativa instantaneamente, o TVSDK armazena um ou mais canais em buffer antes do início da reprodução.

1. Confirme se o recurso foi carregado e está pronto para ser reproduzido verificando se o estado é PREPARADO.
1. Antes de chamar `play`, chame `prepareBuffer` para cada instância `MediaPlayer`.

   Isso ativa o recurso instantâneo, o que significa que os start TVSDK fazem buffering sem reproduzir o recurso de mídia. O TVSDK despacha o evento `BUFFERING_COMPLETED` quando o buffer está cheio.

   >[!NOTE]
   >
   >Por padrão, `prepareBuffer` e `prepareToPlay` configuram o fluxo de mídia para o start reproduzido desde o início. Para start em outra posição, passe a posição (em milissegundos) para `prepareToPlay`.

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

1. Quando você recebe o evento `BUFFERING_COMPLETE`, o start reproduz o item ou exibe o feedback visual para indicar que o conteúdo está completamente armazenado em buffer.

   Se você chamar `play`, a reprodução deve começar imediatamente.

   ```java
   void onBufferPrepared(const psdk::PSDKEvent *ev) { 
       mediaPlayer->play(); 
   }
   ```
