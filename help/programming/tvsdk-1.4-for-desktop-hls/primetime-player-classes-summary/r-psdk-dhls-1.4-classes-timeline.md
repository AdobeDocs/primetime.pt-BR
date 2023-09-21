---
description: Essas classes fornecem informações sobre a linha do tempo de uma mídia específica, incluindo a colocação de anúncios.
title: Classes de linha do tempo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Classes de linha do tempo{#timeline-classes}

Essas classes fornecem informações sobre a linha do tempo de uma mídia específica, incluindo a colocação de anúncios.

Pacote: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/package-detail.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> <p>Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/ContentTracker.html" format="html" scope="external"> ContentTracker </a> </span> </td> 
   <td colname="2"> Interface que define o protocolo que deve ser implementado se você quiser criar um módulo de rastreamento de conteúdo projetado para integrar-se à biblioteca do TVSDK. <p>Essa interface exige que você defina como os eventos de progresso são relatados ao sistema de rastreamento remoto. </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Opportunity.html" format="html" scope="external"> Oportunidade </a> </span> </td> 
   <td colname="2"> Classe base para todas as classes de oportunidade. Uma classe de oportunidade representa um ponto "interessante" na linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Placement.html" format="html" scope="external"> Posicionamento </a> </span> </td> 
   <td colname="2"> Classe que contém informações relacionadas ao posicionamento da linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementMode.html" format="html" scope="external"> PlacementMode </a> </span> </td> 
   <td colname="2"> Enumeração de modos de posicionamento, como inserir ou substituir conteúdo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/PlacementType.html" format="html" scope="external"> PlacementType </a> </span> </td> 
   <td colname="2"> Enumeração de tipos de posicionamento que indicam onde o posicionamento é feito na linha do tempo; por exemplo, PRE_ROLL. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Reservation.html" format="html" scope="external"> Reserva </a> </span> </td> 
   <td colname="2"> Uma reserva é usada para limitar ou impedir o processamento adicional de um determinado intervalo de tempo na linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Linha do tempo </a> </span> </td> 
   <td colname="2"> Interface que fornece um iterador para o processamento de marcadores de linha do tempo. Representa a linha do tempo do conteúdo, incluindo ad breaks. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> ItemDaLinhaDoTempo </a> </span> </td> 
   <td colname="2"> Classe. Representação imutável genérica de um item da linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <span class="codeph"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> MarcadorDeLinhaDoTempo </a> </span> </td> 
   <td colname="2"> Classe que representa um marcador na linha do tempo. Isso marca uma região de interesse no cronograma real. Atualmente, as regiões de interesse são os anúncios, que você pode querer marcar, por exemplo, com uma cor diferente na interface da barra de limpeza. Cada marcador é definido por uma posição e uma duração (cada uma expressa em milissegundos). </td> 
  </tr> 
 </tbody> 
</table>
