---
description: No TVSDK do navegador, você pode buscar uma posição específica (tempo) em um fluxo. Um fluxo pode ser uma lista de reprodução de janela deslizante ou conteúdo de vídeo sob demanda (VOD).
title: Manipular busca ao usar a barra de busca
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---

# Manipular busca ao usar a barra de busca{#handle-seek-when-using-the-seek-bar}

No TVSDK do navegador, você pode buscar uma posição específica (tempo) em um fluxo. Um fluxo pode ser uma lista de reprodução de janela deslizante ou conteúdo de vídeo sob demanda (VOD).

>[!IMPORTANT]
>
>A busca em um stream ao vivo é permitida somente para DVR.

1. Aguarde até que o TVSDK do navegador esteja em um estado válido para busca.

   Os estados válidos são PREPARED, COMPLETE, PAUSED e PLAYING. Estar em um estado válido garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver em um estado pesquisável válido, a tentativa de chamar os métodos a seguir acionará um `IllegalStateException`.

   Por exemplo, você pode esperar que o TVSDK do navegador seja acionado  `AdobePSDK.MediaPlayerStatusChangeEvent`  com um `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Passar a posição de busca solicitada para a `MediaPlayer.seek` como parâmetro em milissegundos.

   Isso move o indicador de reprodução para uma posição diferente no fluxo.

   >[!TIP]
   >
   >A posição de busca solicitada pode não coincidir com a posição real calculada.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Aguarde o TVSDK do navegador acionar o  `AdobePSDK.PSDKEventType.SEEK_END`  evento, que retorna a posição ajustada no evento `actualPosition` atributo:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. Algumas das seguintes regras podem se aplicar:

   * O comportamento da reprodução é afetado se uma busca ou outro reposicionamento terminar no meio de um ad break ou ignorar ad breaks.
   * Você pode buscar somente na duração pesquisável do ativo. Para VOD, isso é de 0 até a duração do ativo.

1. Para a barra de busca criada no exemplo acima, acompanhe `setPositionChangeListener()` para ver quando o usuário está depurando:

   ```js
   seekBar.setPositionChangeListener(function (pos) { 
                   var range = player.seekableRange; 
                   if (range) { 
                       var duration = range.duration; 
                       var time = duration * pos; // seek bar range is [0,1] 
                       player.seek(time); 
   
                       console.log("seek to " + time + " / " + duration); 
                   } 
   
               }); 
   ```

1. Configure retornos de chamada do ouvinte de evento para alterações na atividade de busca do usuário.

       A operação de busca é assíncrona, portanto, o TVSDK do Navegador despacha esses eventos relacionados à busca:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` para indicar que a busca está começando.
   * `AdobePSDK.PSDKEventType.SEEK_END` para indicar que o pedido foi bem-sucedido.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` para indicar que o reprodutor de mídia reajustou a posição de busca fornecida pelo usuário.
