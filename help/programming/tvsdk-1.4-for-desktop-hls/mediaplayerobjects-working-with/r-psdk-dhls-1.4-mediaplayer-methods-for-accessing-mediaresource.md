---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
title: Métodos do MediaPlayer para acessar informações do MediaResource
exl-id: 74e453d6-233e-4146-9f63-ab6919a4ba39
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Métodos do MediaPlayer para acessar informações do MediaResource{#mediaplayer-methods-for-accessing-mediaresource-information}

Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.

<table frame="all" colsep="1" rowsep="1" id="table_77B55D506FE24326A03D97AA087231FF"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="2" class="entry"> Método </th> 
   <th colname="3" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Transmissão ao vivo </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get isLive():Boolean; </span> </td> 
   <td colname="3"> <p>True se o fluxo estiver ativo; false se for VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM protegido</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get isProtected():Boolean; </span> </td> 
   <td colname="3"> <p>True se o fluxo estiver protegido por DRM. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get drmMetadataInfos(): vetor.&lt;drmmetadatainfo&gt;; </span> </td> 
   <td colname="3"> <p>Lista todos os objetos de metadados DRM descobertos no manifesto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Legendas ocultas</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get hasClosedCaptions():Boolean; </span> </td> 
   <td colname="3"> <p>Verdadeiro se as faixas de legendas ocultas estiverem disponíveis. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get closedCaptionsTracks():Vetor.&lt;closedcaptionstrack&gt;; </span> </td> 
   <td colname="3"> <p>Fornece uma lista de faixas de legendas ocultas disponíveis. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get seletedClosedCaptionsTrack():ClosedCaptionsTrack </span> </td> 
   <td colname="3"> <p>Recupera a faixa atual de legendas ocultas selecionada com <span class="codeph"> SelecionarLegendasOcultasRastrear </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack (closedCaptionsTrack: com.adobe.mediacore.info:ClosedCaptionsTrack ) </span> </td> 
   <td colname="3"> <p>Define uma faixa de legendas ocultas para ser a faixa de legendas ocultas atual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Faixas de áudio alternativas </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get hasAlternateAudio():Boolean; </span> </td> 
   <td colname="3"> <p>Verdadeiro se o fluxo tiver faixas de áudio alternativas. </p> <p>Dica: a faixa de áudio principal (padrão) também faz parte da lista de faixas de áudio alternativas. </p> <p>O TVSDK para HLS para desktop considera a faixa de áudio principal um dos itens na lista de faixas de áudio alternativa. Por esse motivo, o único caso em que <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> retorna falso quando o fluxo não tem áudio. Se o conteúdo tiver apenas uma faixa de áudio, esse método retornará true e <span class="codeph"> obter AudioTracks </span> retorna uma lista com um único elemento (a faixa de áudio padrão). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get audioTracks():Vetor.&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> Fornece uma lista de faixas de áudio alternativas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get audioTracks():Vetor.&lt;audiotrack&gt;; </span> </td> 
   <td colname="3"> <p>Fornece uma lista de faixas de áudio alternativas disponíveis. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get seletedAudioTrack():AudioTrack; </span> </td> 
   <td colname="3"> <p>Recupera a faixa de áudio selecionada com <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack(audioTrack: AudioTrack ) </span> </td> 
   <td colname="3"> <p>Seleciona uma faixa de áudio para ser a faixa atual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Metadados cronometrados</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função getTimedMetadata():Boolean; </span> </td> 
   <td colname="3"> <p>True se o fluxo tiver metadados cronometrados associados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get timedMetadata():Vetor.&lt;timedmetadata&gt;; </span> </td> 
   <td colname="3"> <p>Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get isDynamic():Boolean; </span> </td> 
   <td colname="3"> <p>True se o fluxo for um fluxo de taxa de múltiplos bits (MBR). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get profiles():Vetor.&lt;profile&gt;; </span> </td> 
   <td colname="3"> <p>Fornece uma lista dos perfis de taxa de bits associados. Para cada perfil, você pode recuperar sua taxa de bits e a altura e largura do perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Truque </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get isTrickPlaySupported():Boolean; </span> </td> 
   <td colname="3"> <p>True se o reprodutor oferecer suporte para avanço rápido, retrocesso e retomada. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get availablePlaybackRates():Vetor.&lt;Number&gt; </span> </td> 
   <td colname="3"> <p>Fornece a lista de taxas de reprodução disponíveis no contexto do recurso de truque. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Reprodutor de mídia </b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get player():MediaPlayer </span> </td> 
   <td colname="3"> <p>Retorna o reprodutor de mídia atualmente associado a este reprodutor. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Recurso de mídia</b> </td> 
   <td colname="2"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> função get resource():MediaResource; </span> </td> 
   <td colname="3"> <p>Retorna o recurso de mídia associado a este item. </p> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="2"> <span class="codeph"> função get resourceId():int </span> </td> 
   <td colname="3"> <p>Retorna o identificador de mídia associado a este item. </p> </td> 
  </tr> 
 </tbody> 
</table>
