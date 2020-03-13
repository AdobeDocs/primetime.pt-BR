---
description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto no vídeo sob demanda (VOD) quanto nos fluxos ao vivo.
seo-description: O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto no vídeo sob demanda (VOD) quanto nos fluxos ao vivo.
seo-title: Exibir uma barra de depuração de busca com a posição de reprodução atual
title: Exibir uma barra de depuração de busca com a posição de reprodução atual
uuid: f940b305-4893-4531-9a79-53670f5fd23f
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e

---


# Exibir uma barra de depuração de busca com a posição de reprodução atual{#display-a-seek-scrub-bar-with-the-current-playback-position}

O TVSDK oferece suporte à busca para uma posição específica (hora) em que o fluxo é uma lista de reprodução de janela deslizante, tanto no vídeo sob demanda (VOD) quanto nos fluxos ao vivo.

>[!IMPORTANT]
>
>A busca em um fluxo ao vivo é permitida apenas para DVR.

1. Configure retornos de chamada para busca.

       A busca é assíncrona, portanto, o TVSDK despacha os seguintes eventos relacionados à busca:
   
   * `SeekEvent.SEEK_BEGIN` - Procure iniciar.
   * `SeekEvent.SEEK_END` - Busca bem-sucedida.
   * `SeekEvent.SEEK_POSITION_ADJUSTED` - reajusta a posição de busca fornecida pelo usuário.

1. Aguarde o player ter um status válido para busca.

   Os estados válidos são PREPARADO, CONCLUÍDO, PAUSADO e REPRODUZIDO.

1. Analise o evento apropriado para ver quando o usuário está depurando.
1. Passe a posição de busca solicitada (milissegundos) para o `MediaPlayer.seek` método.

   ```
   function seek(position:Number):void;
   ```

   Você pode procurar apenas na duração pesquisável do ativo. Para vídeo sob demanda, a duração é de 0 até a duração do ativo.

   >[!TIP]
   >
   >Isso move o indicador de reprodução para uma nova posição no fluxo, mas a posição final calculada pode diferir da posição de busca especificada.

1. Aguarde o TVSDK despachar o `SeekEvent.SEEK_END` evento.
1. Recupere a posição final de reprodução ajustada usando event.atualPosition.

       Isso é importante porque a posição inicial real após a busca pode ser diferente da posição solicitada. Várias regras podem ser aplicadas, incluindo:
   
   * O comportamento de reprodução é afetado se uma busca ou outro reposicionamento terminar no meio de uma pausa de anúncio ou ignorar quebras de anúncio.
   * Se você buscar perto de um limite de segmento, a posição de busca é ajustada para o início do segmento.

1. Use as informações de posição ao exibir uma barra de depuração de busca.
