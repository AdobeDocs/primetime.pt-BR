---
title: Segurança de camada de rede
description: Segurança de camada de rede
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Segurança de camada de rede{#network-layer-security}

As vulnerabilidades de segurança de rede estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de proteção dos hosts na rede contra essas vulnerabilidades. Ele aborda a segmentação de rede, o fortalecimento da pilha do protocolo de controle de transmissão/protocolo de Internet (TCP/IP) e o uso de firewalls para proteção de host.

Esta tabela descreve técnicas comuns que reduzem as vulnerabilidades de segurança da rede.

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table-djf-lhz-n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Técnica </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Zonas desmilitarizadas (DMZs) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A segmentação deve existir em pelo menos dois níveis com o servidor de aplicativos usado para executar o Acesso ao Adobe, colocado atrás do firewall interno. Separe a rede externa da DMZ que contém os servidores Web, que por sua vez devem ser separados da rede interna. Use firewalls para implementar as camadas de separação. Categorize e controle o tráfego que passa por cada camada de rede para garantir que apenas o mínimo absoluto de dados necessários seja permitido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Endereços IP privados </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use a Conversão de Endereços de Rede (NAT) com endereços IP privados RFC 1918 nos servidores de aplicativos Adobe Access. Atribua endereços IP privados (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) para tornar mais difícil para um invasor rotear o tráfego de e para um host interno NAT pela Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewalls </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use os seguintes critérios para selecionar uma solução de firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implemente firewalls que suportam servidores proxy e/ou inspeção com monitoração de estado em vez de soluções simples de filtragem de pacotes. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Use um firewall compatível com um paradigma de segurança em que você possa negar todos os serviços, exceto aqueles explicitamente permitidos. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implemente uma solução de firewall que seja dual-homed ou multi-homed. Essa arquitetura oferece o mais alto nível de segurança e ajuda a impedir que usuários não autorizados ignorem a segurança do firewall. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>
