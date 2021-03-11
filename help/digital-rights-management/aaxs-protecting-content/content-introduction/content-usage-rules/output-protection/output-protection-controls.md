---
title: Controles de proteção de saída
description: Controles de proteção de saída
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Controles de proteção de saída {#output-protection-controls}

**Controle se a saída para dispositivos de renderização externos está protegida. Especifique saídas analógicas e digitais de maneira independente.**

Controla se a saída para dispositivos de renderização externos deve ser restrita. Um dispositivo externo é definido como qualquer dispositivo de vídeo ou áudio que não esteja incorporado no computador. A lista de dispositivos externos exclui monitores integrados, como em computadores notebook. Restrições de saída analógica e digital podem ser especificadas independentemente.

Estão disponíveis as seguintes opções/níveis de execução:

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Suportado em dispositivos analógicos </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Suportado em dispositivos digitais </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obrigatório</b>  — A proteção de saída Analog Copy Protection (ACP) ou Copy Generation Management System - Analog (CGMS-A) deve ser ativada para reproduzir conteúdo em um dispositivo externo. Os clientes do Adobe Access devem ativar a proteção de saída usando ACP ou CGMS-A. Em dispositivos que suportam ambos, os clientes do Adobe Access 3.0 tentarão habilitar ambos. No entanto, apenas um deve estar habilitado para reproduzir o conteúdo. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP Obrigatório</b>  — É necessária a proteção de saída ACP. A reprodução não é permitida no CGMS-A. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem reprodução" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A Obrigatório</b>  — A proteção de saída CGMS-A é necessária. A reprodução não é permitida em ACP. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem reprodução" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use se disponível</b>  — Tente ativar a proteção de saída ACP e CGMS-A, se disponível, e permita a reprodução, se não estiver disponível. Os clientes do Adobe Access 3.0 tentarão habilitar o ACP e o CGMS-A, se possível. Os clientes do Adobe Access 2.0 só tentarão habilitar o ACP ou o CGMS-A. Por exemplo, uma tentativa será feita pelo cliente Adobe Access para habilitar ACP ou CGMS-A. Se a tentativa for bem-sucedida, a outra opção não será habilitada. Se a tentativa falhar, será feita uma segunda tentativa para habilitar a outra opção. Mesmo que ambas as tentativas falhem, o conteúdo será reproduzido de qualquer maneira. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use ACP se disponível</b>  — Tente ativar a proteção de saída ACP, se disponível, mas permita a reprodução, se não estiver disponível. A proteção não está disponível no CGMS-A. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem proteção" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use o CGMS-A, se disponível  </b>— Tente ativar a proteção de saída do CGMS-A, se disponível, mas permita a reprodução, se não estiver disponível. A proteção não está disponível no ACP. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem proteção" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sem proteção</b> — Nenhuma ativação de proteção de saída é imposta para saídas analógicas e digitais. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sem reprodução</b> : não permita reprodução em um dispositivo externo para saídas analógicas e digitais. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Embora essas regras sejam aplicadas de forma consistente em todas as plataformas, atualmente é possível ativar com segurança a proteção de saída em plataformas Windows. Em outras plataformas (como Macintosh e Linux) não há funções de sistema operacional de suporte disponíveis para aplicativos de terceiros.

Exemplo de caso de uso: Alguns conteúdos podem impor controles de proteção de saída, e o nível de proteção pode ser definido pelo distribuidor de conteúdo. Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada em um Macintosh, o cliente não reproduzirá conteúdo em dispositivos externos. No entanto, o conteúdo será reproduzido em monitores internos.

Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada no Linux, o cliente não reproduzirá o conteúdo em nenhum dispositivo porque não é possível diferenciar entre dispositivos internos e externos.

Se você especificar &quot;Use if available&quot;, a proteção de saída será ativada, quando possível. Por exemplo, em máquinas do Windows que oferecem suporte ao COPP (Certified Output Protection Protocol), o conteúdo é transmitido com proteção de saída para uma exibição externa. Esse exemplo às vezes é conhecido como &quot;controle de saída selecionável&quot;.
