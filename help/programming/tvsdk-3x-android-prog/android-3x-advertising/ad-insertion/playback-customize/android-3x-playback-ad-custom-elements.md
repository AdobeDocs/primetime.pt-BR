---
description: O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.
seo-description: O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.
seo-title: Elementos de API para reprodução de anúncio
title: Elementos de API para reprodução de anúncio
uuid: 56844663-d635-4b04-b61b-cb8f33ef5732
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Elementos de API para reprodução de anúncio {#api-elements-for-ad-playback}

O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.

Os seguintes elementos de API são úteis para personalizar a reprodução:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>Elemento da API </b></th> 
   <th colname="col2" class="entry"> <b>Conteúdo que suporta publicidade</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata </span> </td> 
   <td colname="col2">Controle se uma quebra de anúncio deve ser marcada como assistida por um visualizador e, em caso afirmativo, quando marcá-la. Defina e obtenha a política assistida usando <span class="codeph"> setAdBreakAsWatched</span> e <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera possíveis políticas de reprodução para pausas de anúncio. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera possíveis políticas de reprodução para anúncios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> Interface que permite a personalização do comportamento do anúncio TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Classe que implementa o comportamento padrão do TVSDK. Seu aplicativo pode substituir essa classe para personalizar os comportamentos padrão sem implementar a interface completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>Esta é a hora local da reprodução, exceto as pausas de anúncio inseridas. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> searchToLocal</span>. <p>Aqui, a busca ocorre em relação a uma hora local no fluxo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>A posição virtual na linha do tempo é convertida para a posição local. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> no <span class="codeph"> MediaPlayer</span> retorna a hora atual em relação ao conteúdo original, sem anúncios dinamicamente duplicados. <span class="codeph"> getLocalTime</span> em <span class="codeph"> AdBreak</span> retorna a hora de início da quebra em relação ao conteúdo original. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> propriedade isWatched</span> . Indica se o visualizador assistiu ao anúncio. </td> 
  </tr> 
 </tbody> 
</table>