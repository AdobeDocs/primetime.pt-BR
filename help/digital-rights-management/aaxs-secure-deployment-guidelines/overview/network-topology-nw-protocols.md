---
title: Protocolos de rede usados pelo Adobe Access
description: Protocolos de rede usados pelo Adobe Access
copied-description: true
exl-id: f065690d-6fa1-43a7-8aa8-a1ccd68e998d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Protocolos de rede usados pelo Adobe Access {#network-protocols-used-by-adobe-access}

Quando você configura uma arquitetura de rede segura, os protocolos de rede na tabela a seguir são necessários para a interação entre o Acesso ao Adobe e outros sistemas na sua rede corporativa.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-itc-33z-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Protocolo </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Uso </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTP </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Clientes Flash Player, Adobe AIR® e Adobe Primetime se comunicam com o Acesso Adobe via HTTP. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">HTTPS (opcional) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Os clientes Flash Player, Adobe AIR e Adobe Primetime podem usar HTTPS para comunicação com o Adobe Access; no entanto, HTTPS (SSL) não é necessário, a menos que você precise de suporte para clientes FMRMS 1.x. Ver as notas na tabela <a href="network-topology-firewall-rules.md" format="dita" scope="local"> URLs de entrada</a> e <a href="network-topology-nw-protocols.md"> Configuração do SSL</a>. </p> </td> 
  </tr> 
 </tbody> 
</table>
