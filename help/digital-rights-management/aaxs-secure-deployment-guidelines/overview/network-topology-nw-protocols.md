---
seo-title: Protocolos de rede usados pelo Adobe Access
title: Protocolos de rede usados pelo Adobe Access
uuid: 4f2ee3f5-6758-4fbe-b5cd-cead1e5ccde8
translation-type: tm+mt
source-git-commit: c78d3c87848943a0be3433b2b6a543822a7e1c15
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---


# Protocolos de rede usados pelo Adobe Access {#network-protocols-used-by-adobe-access}

Quando você configura uma arquitetura de rede segura, os protocolos de rede na tabela a seguir são necessários para a interação entre o Acesso ao Adobe e outros sistemas em sua rede corporativa.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocolo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Use </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes Flash Player, Adobe AIR® e Adobe Primetime se comunicam com o Adobe Access via HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (opcional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes Flash Player, Adobe AIR e Adobe Primetime podem usar HTTPS para comunicação com o Adobe Access, no entanto, HTTPS (SSL) não é necessário, a menos que você precise de suporte para clientes FMRMS 1.x. Consulte as notas na tabela <a href="network-topology-firewall-rules.md" format="dita" scope="local"> URLs de entrada</a> e <a href="network-topology-nw-protocols.md"> Configurando SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>