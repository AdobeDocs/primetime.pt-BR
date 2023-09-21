---
description: Seu aplicativo pode monitorar a atividade no reprodutor e as alterações no estado dele, ouvindo eventos despachados pelo TVSDK.
title: Eventos de reprodução
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---

# Eventos de reprodução {#playback-events}

Seu aplicativo pode monitorar a atividade no reprodutor e as alterações no estado dele, ouvindo eventos despachados pelo TVSDK.

O TVSDK despacha eventos de reprodução quando ocorrem operações de reprodução de mídia, como o início da reprodução de um vídeo. Para ser notificado sobre todos os eventos relacionados à reprodução, registre os ouvintes com o `MediaPlayer` para os eventos a seguir.

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
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_SELECTED" format="html" scope="external"> RATE_SELETED</a> </td> 
   <td colname="2"> O usuário ou TVSDK selecionou uma nova taxa de reprodução, como avançar, retroceder ou retomar a reprodução em uma velocidade normal. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">PlaybackRateEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/PlaybackRateEvent.html#RATE_PLAYING" format="html" scope="external"> RATE_PLAYING</a> </td> 
   <td colname="2"> Uma nova taxa de reprodução está visível na tela. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> TimeChangeEvent.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimeChangeEvent.html#TIME_CHANGED" format="html" scope="external"> TIME_CHANGED</a> </td> 
   <td colname="2"> A posição atual do indicador de reprodução da mídia foi alterada. Despachado periodicamente quando a hora atual mudar, a cada 250 ms ou mais. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Reprodutor de mídia</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ChangeEvent de MediaPlayerStatus.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerStatusChangeEvent.html#STATUS_CHANGED" format="html" scope="external"> STATUS_CHANGED</a> </td> 
   <td colname="2"> O status do reprodutor de mídia foi alterado. Seu aplicativo deve manipular erros no retorno de chamada deste evento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento de perfil.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/ProfileEvent.html#PROFILE_CHANGED" format="html" scope="external"> PERFIL_ALTERADO</a> </td> 
   <td colname="2">O perfil atual do reprodutor de mídia foi alterado. Use o <span class="codeph"> ProfileEvent.profile</span> para obter o novo perfil que está sendo reproduzido. Use o <span class="codeph"> hora</span> propriedade para obter a hora em que esse evento ocorreu. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>MediaplayerItem</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_CREATED" format="html" scope="external"> ITEM_CREATED</a> </td> 
   <td colname="2">A <span class="codeph"> MediaPlayerItem</span> foi criado. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#ITEM_UPDATED" format="html" scope="external"> ITEM_UPDATED</a> </td> 
   <td colname="2">O reprodutor de mídia atualizou com êxito a mídia em um destes casos: 
    <ul id="ul_E4D1A1D468544C3B9F8046E9B68A956D"> 
     <li id="li_35A2A417BF924E039D9CB36CFBCDFEB6">Quando ocorre uma atualização de manifesto para um ativo ativo ativo. </li> 
     <li id="li_E7AB380C212B4011B07C3B313282681C">Quando um VOD ou ativo ao vivo tem legendas ocultas e a atividade é descoberta pela primeira vez para uma faixa de legendas ocultas. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Legendas e áudio</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Evento MediaPlayerItem.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/MediaPlayerItemEvent.html#CAPTION_UPDATED" format="html" scope="external"> LEGENDA_ATUALIZADA</a> </td> 
   <td colname="2">Foi detectada uma nova faixa de legendas ocultas no fluxo de mídia e na <span class="codeph"> closedCaptionsTracks</span> A coleção foi atualizada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>Manifesto e linha do tempo</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="0"> 
   <td colname="1">EventoDeLinhaDoTempo.<a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/TimelineEvent.html#TIMELINE_UPDATED" format="html" scope="external"> LINHA DO TEMPO_ATUALIZADA</a> </td> 
   <td colname="2">O reprodutor de mídia adicionou ou removeu anúncios, portanto, ele tem uma linha do tempo atualizada. <p>O manifesto atualizado para um ativo ao vivo e ad breaks antigos foram removidos da linha do tempo ou novas oportunidades de anúncio (pontos de sinalização) foram descobertas. O reprodutor de mídia tenta resolver e colocar quaisquer novos anúncios na linha do tempo. </p> <p> Use esse evento para verificar se a linha do tempo tem alguma atualização (o VOD não é alterado durante a reprodução). Em seguida, é possível recuperar a linha do tempo usando <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayer.html#timeline" format="html" scope="external"> MediaPlayer.timeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
