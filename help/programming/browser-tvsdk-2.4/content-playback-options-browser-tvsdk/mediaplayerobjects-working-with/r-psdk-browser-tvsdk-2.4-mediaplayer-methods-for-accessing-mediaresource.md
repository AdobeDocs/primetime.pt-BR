---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo que é representado por um MediaResource carregado.
seo-description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo que é representado por um MediaResource carregado.
seo-title: Atributos do MediaPlayer para acessar informações do MediaResource
title: Atributos do MediaPlayer para acessar informações do MediaResource
uuid: d26f39d6-0a6b-4072-b99a-8767a511a846
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Atributos do MediaPlayer para acessar informações do MediaResource{#mediaplayer-attributes-to-access-mediaresource-information}

Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo que é representado por um MediaResource carregado.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Propósito </th> 
   <th colname="2" class="entry"> Atributo </th> 
   <th colname="3" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Fluxo ao vivo </td> 
   <td colname="2"> <span class="codeph"> live </span> </td> 
   <td colname="3"> True se o fluxo for ao vivo; false se for VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Legendas ocultas </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions </span> </td> 
   <td colname="3"> True se as faixas de legenda fechada estiverem disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks </span> </td> 
   <td colname="3"> Fornece uma lista de faixas de legenda disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> seletedClosedCaptionsTrack </span> </td> 
   <td colname="3"> Recupera a faixa de legenda fechada selecionada com <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Áudio alternativo </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio </span> </td> 
   <td colname="3"> <p>True se o fluxo tiver faixas de áudio alternativas. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks </span> </td> 
   <td colname="3"> Fornece uma lista de trilhas de áudio alternativas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> seletedAudioTrack </span> </td> 
   <td colname="3"> 
    <pre>
      Recupera a faixa de áudio atualmente selecionada que foi selecionada com <span class="codeph"> selectAudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Metadados cronometrados </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata </span> </td> 
   <td colname="3"> True se o fluxo tiver metadados cronometrados associados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata </span> </td> 
   <td colname="3"> Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Vários perfis (taxas de bits) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> perfis </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Fornece uma lista dos perfis de taxa de bits associados a esse fluxo. <p>Observação:  Você pode recuperar a taxa de bits para cada perfil e a altura e largura do perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Recurso de mídia </td> 
   <td colname="2"> <span class="codeph"> recurso </span> </td> 
   <td colname="3"> Retorna o recurso de mídia associado a este item. </td> 
  </tr> 
 </tbody> 
</table>

