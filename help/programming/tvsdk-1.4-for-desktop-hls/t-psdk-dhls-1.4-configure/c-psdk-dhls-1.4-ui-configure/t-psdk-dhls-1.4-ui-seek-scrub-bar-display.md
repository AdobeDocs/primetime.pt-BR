---
description: O TVSDK permite a busca em uma posição específica (tempo) em que o fluxo é uma lista de reprodução de janela deslizante, em fluxos de vídeo sob demanda (VOD) e ao vivo.
title: Exibir uma barra de limpeza de busca com a posição de reprodução atual
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---

# Exibir uma barra de limpeza de busca com a posição de reprodução atual{#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK permite a busca em uma posição específica (tempo) em que o fluxo é uma lista de reprodução de janela deslizante, em fluxos de vídeo sob demanda (VOD) e ao vivo.

>[!IMPORTANT]
>
>A busca em um stream ao vivo é permitida somente para DVR.

1. Configure retornos de chamada para busca.

       A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:
   
   * `SeekEvent.SEEK_BEGIN` - Início da busca.
   * `SeekEvent.SEEK_END` - Busca bem-sucedida.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - reajustou a posição de busca fornecida pelo usuário.

1. Aguarde até que o reprodutor esteja em um status válido para busca.

   Os estados válidos são PREPARED, COMPLETED, PAUSED e PLAYING.

1. Analise o evento apropriado para ver quando o usuário está depurando.
1. Transmita a posição de busca solicitada (milissegundos) para a `MediaPlayer.seek` método.

   ```
   function seek(position:Number):void;
   ```

   Você pode buscar somente na duração pesquisável do ativo. Para vídeos sob demanda, a duração é de 0 até a duração do ativo.

   >[!TIP]
   >
   >Isso move o indicador de reprodução para uma nova posição no fluxo, mas a posição calculada final pode diferir da posição de busca especificada.

1. Aguarde o TVSDK despachar o `SeekEvent.SEEK_END` evento.
1. Recupere a posição de reprodução ajustada final usando event.atualPosition.

       Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. Várias regras podem ser aplicadas, incluindo:
   
   * O comportamento da reprodução é afetado se uma busca ou outro reposicionamento terminar no meio de um ad break ou ignorar ad breaks.
   * Se você buscar perto de um limite de segmento, a posição de busca será ajustada para o início do segmento.

1. Use as informações de posição ao exibir uma barra de limpeza de busca.
