---
seo-title: Segurança da camada de rede
title: Segurança da camada de rede
uuid: bd53bccf-1130-4189-97ec-4259bd25762f
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61

---


# Segurança da camada de rede{#network-layer-security}

As vulnerabilidades de segurança de rede estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet. Esta seção descreve o processo de endurecimento de hosts na rede contra essas vulnerabilidades. Ele aborda a segmentação de rede, o endurecimento da pilha do protocolo de controle de transmissão/protocolo TCP/IP e o uso de firewalls para proteção de host.

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
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A segmentação deve existir em pelo menos dois níveis com o servidor de aplicativos usado para executar o Adobe Access colocado atrás do firewall interno. Separe a rede externa da DMZ que contém os servidores da Web, que, por sua vez, devem ser separados da rede interna. Use firewalls para implementar as camadas de separação. Categorize e controle o tráfego que passa por cada camada de rede para garantir que somente o mínimo absoluto de dados necessários seja permitido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Endereços IP privados </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use a tradução de endereço de rede (NAT) com endereços IP privados RFC 1918 nos servidores de aplicativos do Adobe Access. Atribua endereços IP privados (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) para tornar mais difícil para um invasor rotear tráfego de e para um host interno NAT pela Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewalls </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use os seguintes critérios para selecionar uma solução de firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul-wjf-lhz-n4"> 
      <li class="- topic/li " id="li-8031632160F44037B092988183139202"> <p class="- topic/p ">Implemente firewalls que suportam servidores proxy e/ou inspeção de estado em vez de soluções simples de filtragem de pacotes. </p> </li> 
      <li class="- topic/li " id="li-B65CBB92113E4503B79EB194C34FCA50"> <p class="- topic/p ">Use um firewall que suporte um paradigma de segurança no qual você pode negar todos os serviços, exceto aqueles explicitamente permitidos. </p> </li> 
      <li class="- topic/li " id="li-5CE4C7B65D84410DB4BE966FD8922993"> <p class="- topic/p ">Implemente uma solução de firewall que seja dual-homed ou multi-homed. Essa arquitetura oferece o maior nível de segurança e ajuda a impedir que usuários não autorizados ignorem a segurança do firewall. </p> </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

