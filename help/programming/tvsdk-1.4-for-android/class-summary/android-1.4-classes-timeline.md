---
description: Essas classes fornecem informações sobre a linha do tempo de uma mídia específica, incluindo o posicionamento dos anúncios.
title: Classes de linha do tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---


# Classes de linha do tempo{#timeline-classes}

Essas classes fornecem informações sobre a linha do tempo de uma mídia específica, incluindo o posicionamento dos anúncios.

Pacote: [com.adobe.mediacore.timeline](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/package-summary.html)

<table frame="all" colsep="1" rowsep="1" id="table_6752E908BA6546549619994A3F7D5F87"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> Nome </th> 
   <th colname="2" class="entry"> <p>Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/PlacementOpportunity.html" format="html" scope="external"> PlacementOpportunity</a></span> </td> 
   <td colname="2"> Uma classe de oportunidade representa um ponto de interesse na linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Linha do tempo</a> </td> 
   <td colname="2"> Interface que fornece um iterador para processar marcadores de linha do tempo. Representa a linha do tempo do conteúdo, incluindo ad breaks. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> ItemLinhaTempo</a> </span> </td> 
   <td colname="2"> Classe. Representação imutável genérica de um item de linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> TimelineMarker</a> </span> </td> 
   <td colname="2"> Interface que representa um marcador na linha do tempo. Isso marca uma região de interesse na linha do tempo real. Atualmente, as regiões de interesse são os anúncios, que você pode querer marcar, por exemplo, com uma cor diferente na interface do usuário da barra de depuração. Cada marcador é definido por uma posição e uma duração (cada uma expressa em milissegundos). </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineOperation.html" format="html" scope="external"> OperaçãoLinhaTempo</a> </td> 
   <td colname="2"> Classe base para todas as operações que afetam a linha do tempo. </td> 
  </tr> 
 </tbody> 
</table>

