---
description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto em fluxos de vídeo sob demanda (VOD) quanto em tempo real.
title: Exibir uma barra de movimentação com a posição de reprodução atual
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 0%

---


# Exibir uma barra de movimentação com a posição de reprodução atual{#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto em fluxos de vídeo sob demanda (VOD) quanto em tempo real.

>[!IMPORTANT]
>
>A busca em direto só é permitida para DVR.

1. Configurar retornos de chamada para busca.

       A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:
   
   * `SeekEvent.SEEK_BEGIN` - Busca a começar.
   * `SeekEvent.SEEK_END` - Busca bem-sucedida.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - reajuste da posição de busca fornecida pelo usuário.

1. Aguarde até que o reprodutor esteja em um status válido para busca.

   Os estados válidos são PREPARADOS, CONCLUÍDOS, PAUSADOS e REPRODUZIDOS.

1. Analise o evento apropriado para ver quando o usuário está depurando.
1. Passe a posição de busca solicitada (milissegundos) para o método `MediaPlayer.seek`.

   ```
   function seek(position:Number):void;
   ```

   Você pode procurar somente na duração pesquisável do ativo. Para vídeo sob demanda, a duração é de 0 até a duração do ativo.

   >[!TIP]
   >
   >Isso move o indicador de reprodução para uma nova posição no fluxo, mas a posição final calculada pode ser diferente da posição de busca especificada.

1. Aguarde o TVSDK despachar o evento `SeekEvent.SEEK_END`.
1. Recupere a posição final ajustada de reprodução usando event.atualPosition.

       Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. Várias regras podem se aplicar, incluindo:
   
   * O comportamento de reprodução é afetado se uma busca ou outro reposicionamento terminar no meio de um ad break ou ignorar ad breaks.
   * Se você procurar perto de um limite de segmento, a posição da busca é ajustada ao início do segmento.

1. Use as informações de posição ao exibir uma barra de movimentação.
