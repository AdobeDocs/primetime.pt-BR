---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
title: Métodos MediaPlayerItem para acessar informações de MediaResource
exl-id: 5e4434ce-d2b1-4b7b-b3d1-77f62ff46d36
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '444'
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
   <td colname="2"> <b>Tags de publicidade</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;string&gt; getAdTags() </span> </td> 
   <td colname="3"> Fornece a lista de tags de anúncio usadas para o processo de posicionamento do anúncio. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Transmissão ao vivo</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> isLive() booleano; </span> </td> 
   <td colname="3"> True se o fluxo estiver ativo; false se for VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>DRM protegido</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano isProtected(); </span> </td> 
   <td colname="3"> True se o fluxo estiver protegido por DRM. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;drmmetadatainfo&gt; getDRMMetadataInfos(); </span> </td> 
   <td colname="3"> Lista todos os objetos de metadados DRM descobertos no manifesto. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Legendas ocultas</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasClosedCaptions(); </span> </td> 
   <td colname="3"> Verdadeiro se as faixas de legendas ocultas estiverem disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;closedcaptionstrack&gt; getClosedCationsTracks(); </span> </td> 
   <td colname="3"> Fornece uma lista de faixas de legendas ocultas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack obtém SeletedClosedCaptionsTrack(); </span> </td> 
   <td colname="3"> Recupera a faixa atual de legendas ocultas selecionada com <span class="codeph"> SelecionarLegendasOcultasRastrear </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack) </span> </td> 
   <td colname="3"> Define uma faixa de legendas ocultas para ser a faixa de legendas ocultas atual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Faixas de áudio alternativas</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio(); </span> </td> 
   <td colname="3"> Verdadeiro se o fluxo tiver faixas de áudio alternativas. <p>Observação: a faixa de áudio principal (padrão) também faz parte da lista de faixas de áudio alternativas. </p> <p>O TVSDK para Android considera a faixa de áudio principal um dos itens na lista de faixas de áudio alternativas. Por esse motivo, o único caso em que <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> retorna falso quando o fluxo não tem áudio. Se o conteúdo tiver apenas uma faixa de áudio, esse método retornará true e <span class="codeph"> MediaPlayerItem.getAudioTracks </span> retorna uma lista com um único elemento (a faixa de áudio padrão). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;audiotrack&gt; getAudioTracks(); </span> </td> 
   <td colname="3"> Fornece uma lista de faixas de áudio alternativas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSelectedAudioTrack(); </span> </td> 
   <td colname="3"> Recupera a faixa de áudio selecionada com <span class="codeph"> selectAudioTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack ) </span> </td> 
   <td colname="3"> Seleciona uma faixa de áudio para ser a faixa atual. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Metadados cronometrados</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasTimedMetadata(); </span> </td> 
   <td colname="3"> True se o fluxo tiver metadados cronometrados associados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;timedmetadata&gt; getTimedMetadata(); </span> </td> 
   <td colname="3"> Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Vários perfis (taxas de bits)</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> isDynamic(); booleano </span> </td> 
   <td colname="3"> True se o fluxo for um fluxo de taxa de múltiplos bits (MBR). </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Lista&lt;profile&gt; getProfiles(); </span> </td> 
   <td colname="3"> Fornece uma lista dos perfis de taxa de bits associados. Para cada perfil, você pode recuperar sua taxa de bits e a altura e largura do perfil. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Perfil getSelectedProfile() </span> </td> 
   <td colname="3"> Recupera o perfil selecionado no momento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Truque</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> isTrickPlaySupported(); booleano </span> </td> 
   <td colname="3"> True se o reprodutor oferecer suporte para avanço rápido, retrocesso e retomada. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> List&lt; Float&gt; getAvailablePlaybackRates() </span> </td> 
   <td colname="3"> Fornece a lista de taxas de reprodução disponíveis no contexto do recurso de truque. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Flutuar getSelectedPlaybackRate() </span> </td> 
   <td colname="3"> Recupera a taxa de reprodução selecionada no momento. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaPlayerItemConfig getConfig() </span> </td> 
   <td colname="3"> Retorna a variável <span class="codeph"> MediaPlayerItemConfig </span> instância associada a este item. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <b>Recurso de mídia</b> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource(); </span> </td> 
   <td colname="3"> Retorna o recurso de mídia associado a este item. </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> int getResourceId() </span> </td> 
   <td colname="3"> Retorna o identificador de mídia associado a este item. Essa ID é definida quando o item é carregado usando <span class="codeph"> MediaPlayerItemLoader.load </span>. </td> 
  </tr> 
 </tbody> 
</table>
