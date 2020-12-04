---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
seo-description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
seo-title: Métodos MediaPlayer para acessar informações de MediaResource
title: Métodos MediaPlayer para acessar informações de MediaResource
uuid: 5d83491c-6577-46fe-98af-83f0fde7a7d0
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '431'
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
   <td colname="1"> <b>Tags de anúncio</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;string&gt; ListgetAdTags()  </span> </td> 
   <td colname="3"> <p>Fornece a lista de tags de anúncio usadas no processo de posicionamento do anúncio. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Fluxo ao vivo</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isLive();  </span> </td> 
   <td colname="3"> <p>True se o fluxo for ao vivo; false se for VOD. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>DRM protegido</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isProtected();  </span> </td> 
   <td colname="3"> <p>True se o fluxo estiver protegido por DRM. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;drmmetadatainfo&gt; ListgetDRMMetadataInfos();  </span> </td> 
   <td colname="3"> <p>Lista todos os objetos de metadados DRM detectados no manifesto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Legendas ocultas</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasClosedCaptions();  </span> </td> 
   <td colname="3"> <p>True se as faixas de legenda fechada estiverem disponíveis. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;closedcaptionstrack&gt; ListgetClosedCationsTracks();  </span> </td> 
   <td colname="3"> <p>Fornece uma lista de faixas de legenda disponíveis. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> ClosedCaptionsTrack get SeletedCaptionsTrack();  </span> </td> 
   <td colname="3"> <p>Recupera o rastreamento de legenda fechada atual selecionado com <span class="codeph"> SelectClosedCaptionsTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectClosedCaptionsTrack ( ClosedCaptionsTrack closedCaptionsTrack)  </span> </td> 
   <td colname="3"> <p>Define uma faixa de legenda fechada para ser a faixa de legenda fechada atual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Faixas de áudio alternativas</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> booleano hasAlternateAudio();  </span> </td> 
   <td colname="3"> <p>True se o fluxo tiver faixas de áudio alternativas. </p> <p>Dica:  A faixa de áudio principal (padrão) também faz parte da lista de faixa de áudio alternativa. </p> <p>O TVSDK para Android considera que a faixa de áudio principal é um dos itens na lista de faixa de áudio alternativa. Por esse motivo, o único caso em que <span class="codeph"> MediaPlayerItem.hasAlternateAudio </span> retorna false é quando o fluxo não tem nenhum áudio. Se o conteúdo tiver apenas uma faixa de áudio, esse método retornará true e <span class="codeph"> MediaPlayerItem.getAudioTracks </span> retornará uma lista com um único elemento (a faixa de áudio padrão). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> Fornece uma lista de trilhas de áudio alternativas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;audiotrack&gt; ListgetAudioTracks();  </span> </td> 
   <td colname="3"> <p>Fornece uma lista de trilhas de áudio alternativas disponíveis. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> AudioTrack getSeletedAudioTrack();  </span> </td> 
   <td colname="3"> <p>Recupera a faixa de áudio selecionada com <span class="codeph"> selectAudioTrack </span>. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> selectAudioTrack ( AudioTrack audioTrack )  </span> </td> 
   <td colname="3"> <p>Seleciona uma faixa de áudio para ser a faixa de áudio atual. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Metadados cronometrados</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean hasTimedMetadata();  </span> </td> 
   <td colname="3"> <p>True se o fluxo tiver metadados cronometrados associados. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;timedmetadata&gt; ListgetTimedMetadata();  </span> </td> 
   <td colname="3"> <p>Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isDynamic();  </span> </td> 
   <td colname="3"> <p>True se o fluxo for um fluxo de taxa de bits múltipla (MBR). </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> &lt;profile&gt; ListgetProfiles();  </span> </td> 
   <td colname="3"> <p>Fornece uma lista dos perfis de taxa de bits associados. Para cada perfil, é possível recuperar sua taxa de bits e a altura e a largura do perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>peça</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> boolean isTrickPlaySupported();  </span> </td> 
   <td colname="3"> <p>Verdadeiro se o player suportar avanço rápido, retrocesso e retomada. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> Taxas&lt; Float=""&gt; deReproduçãoDisponíveisListget  </span> </td> 
   <td colname="3"> <p>Fornece a lista das taxas de reprodução disponíveis no contexto do recurso de peça-play. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <b>Recurso de mídia</b> </td> 
   <td colname="3"> </td>
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> MediaResource getResource();  </span> </td> 
   <td colname="3"> <p>Retorna o recurso de mídia associado a este item. </p> </td> 
  </tr> 
 </tbody> 
</table>

