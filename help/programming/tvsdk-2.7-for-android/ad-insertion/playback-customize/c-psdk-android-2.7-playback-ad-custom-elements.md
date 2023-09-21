---
description: O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.
title: Elementos da API para reprodução de anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Elementos da API para reprodução de anúncio {#api-elements-for-ad-playback}

O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.

Os seguintes elementos de API são úteis para personalizar a reprodução:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento de API </th> 
   <th colname="col2" class="entry"> Conteúdo que suporta publicidade </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdvertisingMetadata </span> </td> 
   <td colname="col2">Controla se um ad break deve ser marcado como tendo sido assistido por um visualizador e, em caso afirmativo, quando marcá-lo. Definir e obter a política observada usando <span class="codeph"> setAdBreakAsWatched</span> e <span class="codeph"> getAdBreakAsWatched</span>. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera possíveis políticas de reprodução para ad breaks. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera possíveis políticas de reprodução para anúncios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdPolicySelector </span> </td> 
   <td colname="col2"> Interface que permite a personalização do comportamento de anúncio do TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> DefaultAdPolicySelector </span> </td> 
   <td colname="col2"> Classe que implementa o comportamento padrão do TVSDK. Seu aplicativo pode substituir essa classe para personalizar os comportamentos padrão sem implementar a interface completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="apiname"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> getLocalTime</span> <p>Essa é a hora local da reprodução, exceto os ad breaks colocados. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"><span class="codeph"> seekToLocal</span>. <p>Aqui, a busca ocorre em relação a uma hora local no fluxo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.convertToLocalTime</span>. <p>A posição virtual na linha do tempo é convertida na posição local. </p> </li> 
    </ul> <p>Importante:  <span class="codeph"> getLocalTime</span> in <span class="codeph"> MediaPlayer</span> retorna a hora atual em relação ao conteúdo original, sem anúncios distribuídos dinamicamente. <span class="codeph"> getLocalTime</span> in <span class="codeph"> AdBreak</span> retorna a hora de início da interrupção relativa ao conteúdo original. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="apiname"> AdBreak</span> </td> 
   <td colname="col2"><span class="codeph"> isWatched</span> propriedade. Indica se o visualizador assistiu ao anúncio. </td> 
  </tr> 
 </tbody> 
</table>
