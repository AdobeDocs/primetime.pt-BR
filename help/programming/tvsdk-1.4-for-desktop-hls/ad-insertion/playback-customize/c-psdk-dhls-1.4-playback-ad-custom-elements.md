---
description: O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.
title: Elementos de API para reprodução do anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Elementos de API para reprodução de anúncio{#api-elements-for-ad-playback}

O TVSDK fornece classes e métodos que você pode usar para personalizar o comportamento de reprodução do conteúdo que contém publicidade.

Os seguintes elementos da API são úteis para personalizar a reprodução:

<table id="table_B07E373B9D2B425AB36466B1D42411AD"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Elemento da API </th> 
   <th colname="col2" class="entry"> Conteúdo compatível com publicidade </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdvertisingMetadata</span> </td> 
   <td colname="col2">Controle se um ad break deve ser marcado como visto por um visualizador e, em caso positivo, quando marcá-lo. Defina e obtenha a política assistida usando 
    <pre>
     o 
     Propriedade <span class="codeph"> adBreakAsWatched</span>.
    </pre> </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdBreakPolicy</span> </td> 
   <td colname="col2"> Enumera possíveis políticas de reprodução para ad breaks. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicy</span> </td> 
   <td colname="col2"> Enumera possíveis políticas de reprodução para anúncios. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> AdPolicySelector</span> </td> 
   <td colname="col2"> Interface que permite a personalização do comportamento do anúncio TVSDK. </td> 
  </tr> 
  <tr> 
   <td colname="col1"><span class="codeph"> DefaultAdPolicySelector</span> </td> 
   <td colname="col2"> Classe que implementa o comportamento padrão do TVSDK. Seu aplicativo pode substituir essa classe para personalizar os comportamentos padrão sem implementar a interface completa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> MediaPlayer</span> </td> 
   <td colname="col2"> 
    <ul id="ul_37700A741403448A8760FDDA68B099AA"> 
     <li id="li_B465170D449E49489C5924572BEEB4A5"><span class="codeph"> localTime</span>. <p>Esse é o horário local da reprodução, excluindo as quebras de anúncio. </p> </li> 
     <li id="li_D9D68CF428904BB2B84E1BCE828A90DC"> <span class="codeph"> searchToLocal</span>. <p>Aqui, a busca ocorre em relação a um horário local no fluxo. </p> </li> 
     <li id="li_9DBCA75537DC4824AA66B53A3FA28812"><span class="codeph"> getTimeline.conversionToLocalTime</span>. <p>A posição virtual na linha do tempo é convertida para a posição local. </p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> ItemLinhaTempo</span> </td> 
   <td colname="col2"> 
    <ul id="ul_99AD34F823DB4F10937EE39DAD0C0B72"> 
     <li id="li_87E2DA15ECE74CFE9C9FBBE8F4B62440"><span class="codeph"> vigiado</span>. <p>Indica se o visualizador assistiu ao anúncio. </p> </li> 
     <li id="li_A9E5A9CF701C48BC94C93F28C114778D"><span class="codeph"> localRange</span>. <p>A posição inicial e a duração de um ad break ou anúncio em relação ao conteúdo original. </p> </li> 
     <li id="li_070BDA0BF4184863AF44652BD5A0CCEC"><span class="codeph"> virtualRange</span>. <p>A posição inicial e a duração de um ad break ou anúncio na linha do tempo virtual, após considerar todas as interrupções de anúncio. </p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

