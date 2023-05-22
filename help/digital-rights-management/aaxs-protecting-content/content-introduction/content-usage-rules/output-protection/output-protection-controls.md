---
title: Controles de proteção de saída
description: Controles de proteção de saída
copied-description: true
exl-id: e27e49f9-9bc3-493f-a9ba-efe623694942
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---

# Controles de proteção de saída {#output-protection-controls}

**Controla se a saída para dispositivos de renderização externos está protegida. Especifique independentemente as saídas analógica e digital.**

Controla se a saída para dispositivos de renderização externos deve ser restrita. Um dispositivo externo é definido como qualquer dispositivo de vídeo ou áudio que não esteja incorporado no computador. A lista de dispositivos externos exclui exibições integradas, como em notebooks. As restrições de saída analógica e digital podem ser especificadas independentemente.

As seguintes opções/níveis de imposição estão disponíveis:

<table frame="all" colsep="0" rowsep="1" id="adobetable_fvw_5fx_n4"> 
 <thead class="- topic/thead "> 
  <tr rowsep="1" class="- topic/row "> 
   <th colname="1" class="- topic/entry entry"> <p class="- topic/p ">Opção </p> </th> 
   <th colname="2" class="- topic/entry entry"> <p class="- topic/p ">Compatível com dispositivos analógicos </p> </th> 
   <th colname="3" class="- topic/entry entry"> <p class="- topic/p ">Compatível com dispositivos digitais </p> </th> 
  </tr> 
 </thead>
 <tbody class="- topic/tbody "> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obrigatório</b> — a proteção de saída Analog Copy Protection (ACP) ou Copy Generation Management System - Analog (CGMS-A) deve estar ativada para reproduzir conteúdo em um dispositivo externo. Os clientes de Acesso ao Adobe devem habilitar a proteção de saída usando ACP ou CGMS-A. Em dispositivos que suportam ambos, os clientes Adobe Access 3.0 tentarão ativar ambos. No entanto, apenas um deve estar habilitado para reproduzir o conteúdo. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP Obrigatório</b> — É necessária a proteção de saída ACP. A reprodução não é permitida no CGMS-A. Os clientes do Adobe Access 2.0 não suportam esta opção. Se definida, um cliente Adobe Access 2.0 se comportará como se a opção "Sem reprodução" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A obrigatório</b> — É necessária a proteção de saída CGMS-A. A reprodução não é permitida no ACP. Os clientes do Adobe Access 2.0 não suportam esta opção. Se definida, um cliente Adobe Access 2.0 se comportará como se a opção "Sem reprodução" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usar se disponível</b> — Tente ativar a proteção de saída ACP e CGMS-A se disponível e permita a reprodução se não estiver disponível. Os clientes do Adobe Access 3.0 tentarão ativar o ACP e o CGMS-A, se possível. Os clientes do Adobe Access 2.0 só tentarão habilitar o ACP ou o CGMS-A. Por exemplo, o cliente de acesso ao Adobe tentará habilitar ACP ou CGMS-A. Se a tentativa for bem-sucedida, a outra opção não será ativada. Se a tentativa falhar, será feita uma segunda tentativa para habilitar a outra opção. Mesmo se ambas as tentativas falharem, o conteúdo será reproduzido mesmo assim. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usar ACP, se disponível</b> — Tentar habilitar a proteção de saída ACP, se disponível, mas permitir reprodução, se não estiver disponível. Proteção não disponível no CGMS-A. Os clientes do Adobe Access 2.0 não suportam esta opção. Se definida, um cliente Adobe Access 2.0 se comportará como se a opção "Sem proteção" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Uso do CGMS-A, se disponível </b>— Tente ativar a proteção de saída CGMS-A, se disponível, mas permita a reprodução, se não estiver disponível. A proteção não está disponível no ACP. Os clientes do Adobe Access 2.0 não suportam esta opção. Se definida, um cliente Adobe Access 2.0 se comportará como se a opção "Sem proteção" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sem proteção</b> — Nenhuma ativação de proteção de saída é imposta para saídas analógicas e digitais. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Nenhuma reprodução</b> —Não permitir reprodução em um dispositivo externo para saídas analógicas e digitais. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Embora essas regras sejam aplicadas consistentemente em todas as plataformas, atualmente só é possível ativar com segurança a proteção de saída nas plataformas Windows. Em outras plataformas (como Macintosh e Linux) não há funções de suporte do sistema operacional disponíveis para aplicativos de terceiros.

Exemplo de caso de uso: algum conteúdo pode aplicar controles de proteção de saída e o nível de proteção pode ser definido pelo distribuidor de conteúdo. Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada em um Macintosh, o cliente não reproduzirá o conteúdo em dispositivos externos. No entanto, o conteúdo será reproduzido nos monitores internos.

Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada no Linux, o cliente não reproduzirá o conteúdo em nenhum dispositivo porque não é possível diferenciar entre dispositivos internos e externos.

Se você especificar &quot;Usar se disponível&quot;, a proteção de saída será ativada sempre que possível. Por exemplo, em máquinas Windows que oferecem suporte ao COPP (Certified Output Protection Protocol), o conteúdo é transmitido com proteção de saída a uma tela externa. Esse exemplo às vezes é conhecido como &quot;controle de saída selecionável&quot;.
