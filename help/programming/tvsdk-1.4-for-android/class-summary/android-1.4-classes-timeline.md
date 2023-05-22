---
description: Essas classes fornecem informações sobre a linha do tempo de uma mídia específica, incluindo a colocação de anúncios.
title: Classes de linha do tempo
exl-id: bb879592-aef2-4adb-acbc-c927133a5cc5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 0%

---

# Classes de linha do tempo{#timeline-classes}

Essas classes fornecem informações sobre a linha do tempo de uma mídia específica, incluindo a colocação de anúncios.

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
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/PlacementOpportunity.html" format="html" scope="external"> OportunidadePosicionamento</a></span> </td> 
   <td colname="2"> Uma classe de oportunidade representa um ponto de interesse na linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/Timeline.html" format="html" scope="external"> Linha do tempo</a> </td> 
   <td colname="2"> Interface que fornece um iterador para processamento de marcadores de linha do tempo. Representa a linha do tempo do conteúdo, incluindo ad breaks. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineItem.html" format="html" scope="external"> ItemDaLinhaDoTempo</a> </span> </td> 
   <td colname="2"> Classe. Representação imutável genérica de um item da linha do tempo. </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineMarker.html" format="html" scope="external"> MarcadorDeLinhaDoTempo</a> </span> </td> 
   <td colname="2"> Interface que representa um marcador na linha do tempo. Isso marca uma região de interesse no cronograma real. Atualmente, as regiões de interesse são os anúncios, que você pode querer marcar, por exemplo, com uma cor diferente na interface da barra de limpeza. Cada marcador é definido por uma posição e uma duração (cada uma expressa em milissegundos). </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/timeline/TimelineOperation.html" format="html" scope="external"> OperaçãoDaLinhaDoTempo</a> </td> 
   <td colname="2"> Classe base para todas as operações que afetam a linha do tempo. </td> 
  </tr> 
 </tbody> 
</table>
