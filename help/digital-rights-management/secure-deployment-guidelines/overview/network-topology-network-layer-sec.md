---
description: As vulnerabilidades de segurança de rede estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet, e você deve endurecer os hosts na rede contra essas vulnerabilidades.
title: Segurança da camada de rede
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---


# Segurança da camada de rede{#network-layer-security}

As vulnerabilidades de segurança de rede estão entre as primeiras ameaças a qualquer servidor de aplicativos voltado para a Internet ou para a intranet, e você deve endurecer os hosts na rede contra essas vulnerabilidades.

Estas são algumas técnicas comuns que reduzem as vulnerabilidades de segurança da rede:

<table frame="all" colsep="1" rowsep="1" class="+ topic/table adobe-d/table " id="table_djf_lhz_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Técnica </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Descrição </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Zonas desmilitarizadas (DMZs) </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">A segmentação deve existir em pelo menos dois níveis com o servidor de aplicativos usado para executar o Adobe Primetime DRM quando o Primetime DRM está atrás do firewall interno. Você deve separar a rede externa da DMZ que inclui os servidores da Web e os servidores da Web devem ser separados da rede interna. Você pode usar firewalls para implementar essas camadas de separação. </p> <p>Você pode categorizar e controlar o tráfego que passa por cada camada de rede para garantir que somente o mínimo absoluto de dados necessários seja permitido. </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Endereços IP privados </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Use a NAT (Network Address Translation, tradução de endereço de rede) com endereços IP privados RFC 1918 nos servidores de aplicativos Primetime DRM. Você pode atribuir endereços IP privados (10.0.0.0/8, 172.16.0.0/12 e 192.168.0.0/16) para tornar mais difícil para um invasor rotear o tráfego de e para um host interno NAT pela Internet. </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p ">Firewalls </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">Estes são alguns critérios a serem considerados ao selecionar uma solução de firewall: </p> <p class="- topic/p "> 
     <ul class="- topic/ul " id="ul_wjf_lhz_n4"> 
      <li class="- topic/li " id="li_A620D0B635384590BA7804F9720D04D0">Implemente firewalls que sejam compatíveis com servidores proxy e/ou inspeção com estado, em vez de soluções simples de filtragem de pacotes. </li> 
      <li class="- topic/li " id="li_3E4F814A30C047539185C23F4F57C282">Use um firewall que ofereça suporte a um paradigma de segurança no qual você possa negar todos os serviços, exceto os explicitamente permitidos. </li> 
      <li class="- topic/li " id="li_96160B3F14C4425397F017AF93FABE32">Implemente uma solução de firewall que seja dual-homed ou multi-homed. Essa arquitetura oferece o maior nível de segurança e impede que usuários não autorizados ignorem a segurança do firewall. </li> 
     </ul> </p> </td> 
  </tr> 
 </tbody> 
</table>

