---
description: No TVSDK do navegador, é possível buscar uma posição (hora) específica em um fluxo. Um fluxo pode ser uma lista de reprodução de janela deslizante ou um conteúdo VOD (Video-on-demand).
seo-description: No TVSDK do navegador, é possível buscar uma posição (hora) específica em um fluxo. Um fluxo pode ser uma lista de reprodução de janela deslizante ou um conteúdo VOD (Video-on-demand).
seo-title: Manipular busca ao usar a barra de busca
title: Manipular busca ao usar a barra de busca
uuid: a7c74141-581f-40a3-9d28-ce56ba56773c
translation-type: tm+mt
source-git-commit: 1985694f99c548284aad6e6b4e070bece230bdf4
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---


# Manipular busca ao usar a barra de busca{#handle-seek-when-using-the-seek-bar}

No TVSDK do navegador, é possível buscar uma posição (hora) específica em um fluxo. Um fluxo pode ser uma lista de reprodução de janela deslizante ou um conteúdo VOD (Video-on-demand).

>[!IMPORTANT]
>
>A busca em um fluxo ao vivo é permitida apenas para DVR.

1. Aguarde o TVSDK do navegador estar em um estado válido para busca.

   Os estados válidos são PREPARADO, COMPLETO, PAUSADO e REPRODUZIDO. Estar em um estado válido garante que o recurso de mídia foi carregado com êxito. Se o player não estiver em um estado de pesquisa válido, tentar chamar os métodos a seguir emite um `IllegalStateException`.

   Por exemplo, você pode aguardar o TVSDK do navegador disparar `AdobePSDK.MediaPlayerStatusChangeEvent` com um `event.status` de `AdobePSDK.MediaPlayerStatus.PREPARED`.

1. Passe a posição de busca solicitada para o `MediaPlayer.seek` método como um parâmetro em milissegundos.

   Isso move o indicador de reprodução para uma posição diferente no stream.

   >[!TIP]
   >
   >A posição de busca solicitada pode não coincidir com a posição efetivamente calculada.

   ```js
   void seek(long position) throws IllegalStateException;
   ```

1. Aguarde o TVSDK do navegador disparar o `AdobePSDK.PSDKEventType.SEEK_END` evento, que retorna a posição ajustada no `actualPosition` atributo do evento:

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.SEEK_END, onSeekComplete); 
   onSeekComplete = function (event) {
       // event.actualPosition
   }
   ```

   Isso é importante porque a posição real do start após a busca pode ser diferente da posição solicitada. Algumas das seguintes regras podem ser aplicadas:

   * O comportamento de reprodução é afetado se uma busca ou outro reposicionamento terminar no meio de uma pausa de anúncio ou ignorar quebras de anúncio.
   * Você pode procurar apenas na duração pesquisável do ativo. Para VOD, é de 0 até a duração do ativo.

1. Para a barra de pesquisa criada no exemplo acima, ouça `setPositionChangeListener()` para ver quando o usuário está depurando:

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

1. Configure retornos de chamada do ouvinte de eventos para alterações na atividade de busca do usuário.

       A operação de busca é assíncrona, portanto o TVSDK do navegador despacha esses eventos relacionados à busca:
   
   * `AdobePSDK.PSDKEventType.SEEK_BEGIN` para indicar que a busca está começando.
   * `AdobePSDK.PSDKEventType.SEEK_END` para indicar que a busca foi bem sucedida.
   * `AdobePSDK.PSDKEventType.SEEK_POSITION_ADJUSTED` para indicar que o media player reajudou a posição de busca fornecida pelo usuário.

