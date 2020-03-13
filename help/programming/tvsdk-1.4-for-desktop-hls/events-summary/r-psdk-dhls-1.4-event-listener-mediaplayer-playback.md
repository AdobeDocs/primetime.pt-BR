---
description: Seu aplicativo pode monitorar a atividade no player e o estado em mudança do player, acompanhando os eventos despachados pelo TVSDK.
seo-description: Seu aplicativo pode monitorar a atividade no player e o estado em mudança do player, acompanhando os eventos despachados pelo TVSDK.
seo-title: Eventos de reprodução
title: Eventos de reprodução
uuid: 6d6491d7-cf25-4130-8388-68b8c028bb71
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventos de reprodução {#playback-events}

Seu aplicativo pode monitorar a atividade no player e o estado em mudança do player, acompanhando os eventos despachados pelo TVSDK.

O TVSDK despacha eventos de reprodução quando ocorrem operações de reprodução de mídia, como um vídeo que começa a ser reproduzido. Para ser notificado sobre todos os eventos relacionados à reprodução, registre os ouvintes com o `MediaPlayer` objeto para os seguintes eventos.

<table frame="all" colsep="1" rowsep="1" id="table_922EEA3DE0BD47BA982E11F890CA0A6B"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Evento </th> 
   <th colname="2" class="entry"> Significado </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reprodução</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELECTED</a> </td> 
   <td colname="2"> O usuário ou TVSDK selecionou uma nova taxa de reprodução, como avançar, retroceder ou reiniciar a reprodução em uma velocidade normal. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> Uma nova taxa de reprodução é visível na tela. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> A posição atual do indicador de reprodução da mídia mudou. Despachado periodicamente quando a hora atual mudou, a cada 250 ms ou mais. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Media Player</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">MediaPlayerStatus ChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> O status do player de mídia foi alterado. Seu aplicativo deve lidar com erros no retorno de chamada deste evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ProfileEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PROFILE_CHANGED</a> </td> 
   <td colname="2">O perfil atual do player de mídia foi alterado. Use a propriedade <span class="codeph"> ProfileEvent.profile</span> para obter o novo perfil que está sendo reproduzido. Use a propriedade <span class="codeph"> time</span> para obter a hora em que esse evento ocorreu. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">Um <span class="codeph"> MediaPlayerItem</span> foi criado. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">O media player foi atualizado com êxito em qualquer um destes casos: 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">Quando ocorre uma atualização do manifesto para um ativo em tempo real. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">Quando um VOD ou ativo ativo tiver legendagem fechada e a atividade for descoberta pela primeira vez para uma faixa de legendagem fechada. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Legendas e áudio</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> CAPTION_UPDATED</a> </td> 
   <td colname="2">Uma nova faixa de legendagem fechada foi detectada no fluxo de mídia e a coleção <span class="codeph"> closedCaptionsTracks</span> foi atualizada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesto e Linha do tempo</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">TimelineEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> TIMELINE_UPDATED</a> </td> 
   <td colname="2">O media player adicionou ou removeu anúncios, portanto, ele tem uma linha do tempo atualizada. <p>O manifesto atualizado para um ativo em tempo real e as quebras de anúncio antigas foram removidas da linha do tempo ou novas oportunidades de anúncio (pontos de sinalização) foram descobertas. O player de mídia tenta resolver e colocar quaisquer novos anúncios na linha do tempo. </p> <p> Use esse evento para verificar se a linha do tempo tem alguma atualização (o VOD não muda durante a reprodução). Você pode recuperar a linha do tempo usando <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>

