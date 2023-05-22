---
description: O TVSDK despacha eventos de reprodução quando ocorrem operações de reprodução de mídia, como o início da reprodução de um vídeo.
title: Eventos de reprodução
exl-id: 675dd444-d58c-4316-9d62-b64e6433b650
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---

# Eventos de reprodução{#playback-events}

O TVSDK despacha eventos de reprodução quando ocorrem operações de reprodução de mídia, como o início da reprodução de um vídeo.

Para ser notificado sobre todos os eventos relacionados à reprodução, registre uma implementação de `MediaPlayer.PlaybackEventListener`, incluindo os seguintes retornos de chamada de evento.

<table frame="all" colsep="1" rowsep="1"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Evento </th> 
   <th colname="2" class="entry"> Significado </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Reprodução</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayComplete%28%29" format="html" scope="external"> onPlayComplete</a> </td> 
   <td colname="2"> O fim de uma fonte de mídia foi atingido. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPlayStart%28%29" format="html" scope="external"> onPlayStart</a> </td> 
   <td colname="2"> A reprodução de uma fonte de mídia foi iniciada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRateSelected%28float%29" format="html" scope="external"> onRateSelected</a> (taxa flutuante) </td> 
   <td colname="2"> O usuário ou TVSDK selecionou uma nova taxa de reprodução, como avançar, retroceder ou retomar a reprodução em uma velocidade normal. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onRatePlaying%28float%29" format="html" scope="external"> onRatePlaying</a> (taxa flutuante) </td> 
   <td colname="2"> Uma nova taxa de reprodução está visível na tela. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Mídia</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onPrepared%28%29" format="html" scope="external"> onPrepared</a> </td> 
   <td colname="2"> O reprodutor de mídia preparou a mídia com êxito. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onSizeAvailable%28long,%20long%29" format="html" scope="external"> onSizeAvailable</a> (altura longa, largura longa) </td> 
   <td colname="2"> O tamanho da mídia está disponível. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Reprodutor de mídia</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onStateChanged%28com.adobe.mediacore.MediaPlayer.PlayerState,com.adobe.mediacore.MediaPlayerNotification%29" format="html" scope="external"> onStateChanged</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlayerState.html" format="html" scope="external"> MediaPlayer.PlayerState</a> estado, <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html" format="html" scope="external"> MediaPlayerNotification</a> notificação) </td> 
   <td colname="2"> O estado do reprodutor de mídia foi alterado. Seu aplicativo deve manipular erros nesse retorno de chamada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onProfileChanged%28long,%20long%29" format="html" scope="external"> onProfileChanged</a> (perfil longo, tempo longo) </td> 
   <td colname="2"> O perfil atual do reprodutor de mídia foi alterado. Use o <span class="codeph"> Perfil</span> para obter o novo perfil que está sendo reproduzido. Use o <span class="codeph"> hora</span> propriedade para obter a hora em que esse evento ocorreu. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>MediaplayerItem</b> </td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onUpdated%28%29" format="html" scope="external"> onUpdated</a> </td> 
   <td colname="2">O reprodutor de mídia atualizou com êxito a mídia em um destes casos: 
    <ul> 
     <li>Quando ocorre uma atualização de manifesto para um ativo ativo ativo.</li> 
     <li>Quando um VOD ou ativo ao vivo tem legendas ocultas e a atividade é descoberta pela primeira vez para uma faixa de legendas ocultas. </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="col1"><b>Manifesto e linha do tempo</b></td> 
   <td colname="col2"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimedMetadata%28com.adobe.mediacore.metadata.TimedMetadata%29" format="html" scope="external"> onTimedMetadata</a> (<a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/metadata/TimedMetadata.html" format="html" scope="external"> TimedMetadata</a> timedMetadata) </td> 
   <td colname="2"> Um novo metadado cronometrado é descoberto no manifesto. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.PlaybackEventListener.html#onTimelineUpdated%28%29" format="html" scope="external"> onTimelineUpdated</a> </td> 
   <td colname="2">O reprodutor de mídia adicionou ou removeu anúncios, portanto, ele tem uma linha do tempo atualizada. <p>O manifesto atualizado para um ativo ao vivo e ad breaks antigos foram removidos da linha do tempo ou novas oportunidades de anúncio (pontos de sinalização) foram descobertas. O reprodutor de mídia tenta resolver e colocar quaisquer novos anúncios na linha do tempo. </p><p> Use esse evento para verificar se a linha do tempo tem alguma atualização (o VOD não é alterado durante a reprodução). Em seguida, é possível recuperar a linha do tempo usando <a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.html#getTimeline%28%29" format="html" scope="external"> MediaPlayer.getTimeline</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
