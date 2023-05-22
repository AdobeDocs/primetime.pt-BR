---
title: Modo de sinalização e intervalo de tempo
description: Modo de sinalização e intervalo de tempo
copied-description: true
exl-id: ccaf345f-63f2-42f1-8558-65c7e0dffa89
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '89'
ht-degree: 0%

---

# Modo de sinalização e intervalo de tempo {#signaling-mode-and-time-range}

<table> 
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> MARCAR </th> 
   <th class="entry"> DELETE </th> 
   <th class="entry"> SUBSTITUIR </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> Gerador de Oportunidade de Intervalo Personalizado </span> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
    &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
      &nbsp;range.end,&nbsp; 
      &nbsp;replaceDuration) 
    </code> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ServerMap </span> Modo de sinalização </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK&nbsp;); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin,&nbsp; 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE&nbsp;); 
    </code> </td> 
   <td> N/D (modo de sinalização CustomRange automático) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ManifestCue </span> Modo de sinalização </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE 
     ); 
    </code> </td> 
   <td> N/D (modo de sinalização CustomRange automático) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CustomRange </span> Modo de sinalização </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.DELETE 
     ); 
    </code> </td> 
   <td> 
    <code>
      placement1&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.CUSTOM_RANGE, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;range.end&nbsp;-&nbsp;range.begin, 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementMode.MARK 
     ); 
     placement2&nbsp;=&nbsp;placement&nbsp;=&nbsp; 
     &nbsp;&nbsp;new&nbsp;Placement(/ 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.MID_ROLL( 
     &nbsp;&nbsp;&nbsp;&nbsp;PlacementType.PRE_ROLL), 
     &nbsp;&nbsp;&nbsp;&nbsp;rangeDuration, 
     &nbsp;&nbsp;&nbsp;&nbsp;placementMode 
     ); 
    </code> </td> 
  </tr> 
 </tbody> 
</table>

<table> 
 <thead> 
  <tr> 
   <th class="entry"> </th> 
   <th class="entry"> MARCAR </th> 
   <th class="entry"> DELETE </th> 
   <th class="entry"> SUBSTITUIR </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <span class="codeph"> OpportunityGenerator do AdSignalingMode </span> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end) 
    </code> </td> 
   <td> 
    <code>
      (range.begin,&nbsp; 
     &nbsp;range.end,&nbsp; 
     &nbsp;replaceDuration) 
    </code> </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ServerMap </span> Modo de sinalização </td> 
   <td> Não presente (anúncio desativado). </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;new&nbsp;Placement( 
     PlacementType.SERVER_MAP, 
     Placement.UNKNOWN_TIME, 
     Placement.UNKNOWN_DURATION, 
     PlacementMode.DEFAULT); 
    </code> </td> 
   <td> N/D (automático) <span class="codeph"> CustomRange </span> modo de sinalização) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> ManifestCue </span> Modo de sinalização </td> 
   <td> Não presente (anúncio desativado). </td> 
   <td> 
    <code>
      placement&nbsp;=&nbsp; 
     &nbsp;new&nbsp;Placement( 
     PlacementType.PRE_ROLL, 
     playhead, 
     Placement.UNKNOWN_DURATION, 
     PlacementMode.DEFAULT); 
    </code> </td> 
   <td> N/D (automático) <span class="codeph"> CustomRange </span> modo de sinalização) </td> 
  </tr> 
  <tr> 
   <td> <span class="codeph"> CustomRange </span> Modo de sinalização </td> 
   <td> Não presente (anúncio desativado). </td> 
   <td> Nenhum </td> 
   <td> Nenhum (cuidado no <span class="codeph"> CustomRangeOpportunityGenerator </span>) </td> 
  </tr> 
 </tbody> 
</table>
