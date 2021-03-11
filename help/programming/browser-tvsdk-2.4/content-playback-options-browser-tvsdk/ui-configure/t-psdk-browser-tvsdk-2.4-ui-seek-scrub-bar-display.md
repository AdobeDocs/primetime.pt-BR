---
description: No TVSDK do navegador, você pode procurar uma posição específica (tempo) em um fluxo. Um fluxo pode ser uma lista de reprodução de janela deslizante ou um conteúdo de VOD (video-on-demand).
title: Lidar com a busca ao usar a barra de busca
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '329'
ht-degree: 0%

---


# Lidar com a busca ao usar a barra de busca{#handle-seek-when-using-the-seek-bar}

No TVSDK do navegador, você pode procurar uma posição específica (tempo) em um fluxo. Um fluxo pode ser uma lista de reprodução de janela deslizante ou um conteúdo de VOD (video-on-demand).

>[!IMPORTANT]
>
>A busca em direto só é permitida para DVR.

1. Aguarde o TVSDK do navegador estar em um estado válido para busca.

   Os estados válidos são PREPARADO, CONCLUÍDO, PAUSADO e REPRODUZINDO. Estar em um estado válido garante que o recurso de mídia tenha sido carregado com êxito. Se o reprodutor não estiver em um estado de busca válido, tentar chamar os métodos a seguir acionará um `IllegalStateException`.

   Por exemplo, você pode esperar pelo TVSDK do navegador disparar `AdobePSDK.MediaPlayerStatusChangeEvent` com um `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Passe a posição de busca solicitada para o método `MediaPlayer.seek` como um parâmetro em milissegundos.

   Isso move o indicador de reprodução para uma posição diferente no fluxo.

   >[!TIP]
   >
   >A posição de busca solicitada pode não coincidir com a posição computada real.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Aguarde o TVSDK do navegador acionar o evento `AdobePSDK.PSDKEventType.SEEK_END`, que retorna a posição ajustada no atributo `actualPosition` do evento:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. Algumas das seguintes regras podem se aplicar:

   * O comportamento de reprodução é afetado se uma busca ou outro reposicionamento terminar no meio de uma pausa de anúncio ou ignorar quebras de anúncio.
   * Você pode procurar somente na duração pesquisável do ativo. Para VOD, é de 0 até a duração do ativo.

1. Para a barra de busca criada no exemplo acima, observe `setPositionChangeListener()` para ver quando o usuário está depurando:

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

       A operação de busca é assíncrona, portanto, o TVSDK do navegador despacha esses eventos relacionados à busca:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` para indicar que a busca está sendo iniciada.
   * `AdobePSDK.PSDKEventType.SEEK_END` para indicar que a busca foi bem-sucedida.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` para indicar que o reprodutor de mídia reajustou a posição de busca fornecida pelo usuário.

