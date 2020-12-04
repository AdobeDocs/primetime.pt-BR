---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
seo-description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
seo-title: Métodos MediaPlayerItem para acessar informações de MediaResource
title: Métodos MediaPlayerItem para acessar informações de MediaResource
uuid: c6e77eb7-cefd-48aa-9373-2b44a96217a5
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---


# Métodos MediaPlayerItem para acessar informações de MediaResource {#mediaplayeritem-methods-for-accessing-mediaresource-information}

Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.

<table frame="all" colsep="1" rowsep="1" id="table_F6006A9167044AC087A6ECB20B8CCD5D"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Método </th> 
   <th colname="3" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Tags de anúncio</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;string&gt; ListgetAdTags()  </span> </td> 
   <td colname="3"> Fornece a lista de tags de anúncio usadas no processo de posicionamento do anúncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Fluxo ao vivo</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive();  </span> </td> 
   <td colname="3"> True se o fluxo for ao vivo; false se for VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM protegido</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected();  </span> </td> 
   <td colname="3"> True se o fluxo estiver protegido por DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;drmmetadatainfo&gt; ListgetDRMMetadataInfos();  </span> </td> 
   <td colname="3"> Lista todos os objetos de metadados DRM detectados no manifesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Legendas ocultas</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions();  </span> </td> 
   <td colname="3"> True se as faixas de legenda fechada estiverem disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;closedcaptionstrack&gt; ListgetClosedCationsTracks();  </span> </td> 
   <td colname="3"> Fornece uma lista de faixas de legenda disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SeletedCaptionsTrack();  </span> </td> 
   <td colname="3"> Recupera o rastreamento de legenda fechada atual selecionado com <span class="codeph"> SelectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack)  </span> </td> 
   <td colname="3"> Define uma faixa de legenda fechada para ser a faixa de legenda fechada atual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Faixas de áudio alternativas</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio();  </span> </td> 
   <td colname="3"> True se o fluxo tiver faixas de áudio alternativas. <p>Observação:  A faixa de áudio principal (padrão) também faz parte da lista de faixa de áudio alternativa. </p> <p>O TVSDK para Android considera que a faixa de áudio principal é um dos itens na lista de faixa de áudio alternativa. Por esse motivo, o único caso em que <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> retorna false é quando o fluxo não tem nenhum áudio. Se o conteúdo tiver apenas uma faixa de áudio, esse método retornará true e <span class="codeph"> MediaPlayerItem.getAudioTracks </span> retornará uma lista com um único elemento (a faixa de áudio padrão). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> Fornece uma lista de trilhas de áudio alternativas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSeletedAudioTrack();  </span> </td> 
   <td colname="3"> Recupera a faixa de áudio selecionada com <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack )  </span> </td> 
   <td colname="3"> Seleciona uma faixa de áudio para ser a faixa de áudio atual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Metadados cronometrados</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata();  </span> </td> 
   <td colname="3"> True se o fluxo tiver metadados cronometrados associados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;timedmetadata&gt; ListgetTimedMetadata();  </span> </td> 
   <td colname="3"> Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Vários perfis (taxas de bits)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic();  </span> </td> 
   <td colname="3"> True se o fluxo for um fluxo de taxa de bits múltipla (MBR). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;profile&gt; ListgetProfiles();  </span> </td> 
   <td colname="3"> Fornece uma lista dos perfis de taxa de bits associados. Para cada perfil, é possível recuperar sua taxa de bits e a altura e a largura do perfil. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Perfil getSeletedProfile()  </span> </td> 
   <td colname="3"> Recupera o perfil selecionado no momento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>peça</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported();  </span> </td> 
   <td colname="3"> Verdadeiro se o player suportar avanço rápido, retrocesso e retomada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt; Float=""&gt; ListgetAvailablePlaybackRates()  </span> </td> 
   <td colname="3"> Fornece a lista das taxas de reprodução disponíveis no contexto do recurso de peça-play. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Flutuar getSeletedPlaybackRate()  </span> </td> 
   <td colname="3"> Recupera a taxa de reprodução atualmente selecionada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig()  </span> </td> 
   <td colname="3"> Retorna a instância <span class="codeph"> MediaPlayerItemConfig </span> associada a este item. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Recurso de mídia</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> Retorna o recurso de mídia associado a este item. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId()  </span> </td> 
   <td colname="3"> Retorna o identificador de mídia associado a este item. Essa ID é definida quando o item é carregado usando <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
