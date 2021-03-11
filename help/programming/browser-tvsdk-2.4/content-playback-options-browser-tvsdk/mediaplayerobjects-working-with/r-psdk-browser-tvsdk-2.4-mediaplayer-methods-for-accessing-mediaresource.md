---
description: Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.
title: Atributos do MediaPlayer para acessar informações do MediaResource
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Atributos do MediaPlayer para acessar as informações do MediaResource{#mediaplayer-attributes-to-access-mediaresource-information}

Os métodos na classe MediaPlayerItem permitem obter informações sobre o fluxo de conteúdo representado por um MediaResource carregado.

<table frame="all" colsep="1" rowsep="1" id="table_46225307CA5B4BB1869576E0B9141E38"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Finalidade </th> 
   <th colname="2" class="entry"> Atributo </th> 
   <th colname="3" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> Live stream </td> 
   <td colname="2"> <span class="codeph"> live  </span> </td> 
   <td colname="3"> Verdadeiro se o fluxo for em tempo real; falso se for VOD. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Legendas ocultas </td> 
   <td colname="2"> <span class="codeph"> hasClosedCaptions  </span> </td> 
   <td colname="3"> True se as faixas de legenda fechada estiverem disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> closedCaptionsTracks  </span> </td> 
   <td colname="3"> Fornece uma lista de faixas de legendas ocultas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> seletedClosedCaptionsTrack  </span> </td> 
   <td colname="3"> Recupera a faixa de legenda fechada que foi selecionada com <span class="codeph"> selectClosedCaptionsTrack </span>. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="2"> Áudio alternativo </td> 
   <td colname="2"> <span class="codeph"> hasAlternateAudio  </span> </td> 
   <td colname="3"> <p>True é verdadeiro se o fluxo tiver trilhas de áudio alternativas. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> audioTracks  </span> </td> 
   <td colname="3"> Fornece uma lista de trilhas de áudio alternativas disponíveis. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> seletedAudioTrack  </span> </td> 
   <td colname="3"> 
    <pre>
      Recupera a faixa de áudio atualmente selecionada com 
     <span class="codeph"> selecione AudioTrack </span>. 
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Metadados cronometrados </td> 
   <td colname="2"> <span class="codeph"> hasTimedMetadata  </span> </td> 
   <td colname="3"> True se o fluxo tiver metadados cronometrados associados. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="2"> <span class="codeph"> timedMetadata  </span> </td> 
   <td colname="3"> Fornece uma lista dos objetos de metadados cronometrados associados ao fluxo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"> Vários perfis (taxas de bits) </td> 
   <td colname="2" morerows="1"> <span class="codeph"> perfis  </span> </td> 
   <td colname="3"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="3"> Fornece uma lista dos perfis de taxa de bits associados que estão associados a este fluxo. <p>Observação:  Você pode recuperar a taxa de bits para cada perfil e a altura e largura do perfil. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> Recurso de mídia </td> 
   <td colname="2"> <span class="codeph"> recurso  </span> </td> 
   <td colname="3"> Retorna o recurso de mídia associado a este item. </td> 
  </tr> 
 </tbody> 
</table>

