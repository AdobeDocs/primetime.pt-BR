---
seo-title: Controles de proteção de saída
title: Controles de proteção de saída
uuid: 1f4cc617-7f14-4952-8e61-6acbdf01d10e
translation-type: tm+mt
source-git-commit: 1b9792a10ad606b99b6639799ac2aacb707b2af5
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Controles de proteção de saída {#output-protection-controls}

**Controle se a saída para dispositivos de renderização externos está protegida. Especifique saídas analógicas e digitais independentemente.**

Controla se a saída para dispositivos de renderização externos deve ser restrita. Um dispositivo externo é definido como qualquer dispositivo de vídeo ou áudio que não esteja incorporado no computador. A lista de dispositivos externos exclui exibições integradas, como em computadores notebook. As restrições de saída analógica e digital podem ser especificadas independentemente.

As seguintes opções/níveis de aplicação estão disponíveis:

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
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Obrigatório</b> — Proteção de cópia analógica (ACP) ou Sistema de gerenciamento de geração de cópias - a proteção de saída analógica (CGMS-A) deve ser ativada para reproduzir conteúdo em um dispositivo externo. Os clientes de Acesso a Adobe devem ativar a proteção de saída usando ACP ou CGMS-A. Em dispositivos compatíveis com ambos, os clientes do Adobe Access 3.0 tentarão habilitar ambos. No entanto, somente um deve estar habilitado para reproduzir o conteúdo. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">ACP obrigatório</b> — A proteção de saída ACP é necessária. A reprodução não é permitida no CGMS-A. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem reprodução" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">CGMS-A Obrigatório</b> — A proteção de saída CGMS-A é necessária. A reprodução não é permitida no ACP. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem reprodução" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use se disponível</b> — Tente ativar a proteção de saída ACP e CGMS-A, se disponível, e permita a reprodução, se não disponível. Os clientes do Adobe Access 3.0 tentarão habilitar ACP e CGMS-A, se possível. Os clientes do Adobe Access 2.0 só tentarão ativar o ACP ou o CGMS-A. Por exemplo, o cliente Adobe Access tentará habilitar ACP ou CGMS-A. Se a tentativa for bem-sucedida, a outra opção não será ativada. Se a tentativa falhar, será feita uma segunda tentativa para habilitar a outra opção. Mesmo se ambas as tentativas falharem, o conteúdo será reproduzido assim mesmo. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Usar ACP se disponível</b> — Tente ativar a proteção de saída ACP, se disponível, mas permita a reprodução, se não disponível. A proteção não está disponível no CGMS-A. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem proteção" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Use CGMS-A se disponível  </b>— Tente ativar a proteção de saída CGMS-A, se disponível, mas permita a reprodução, se não disponível. A proteção não está disponível no ACP. Os clientes do Adobe Access 2.0 não suportam essa opção. Se definido, um cliente do Adobe Access 2.0 se comportará como se a opção "Sem proteção" tivesse sido especificada. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">- </p> </td> 
  </tr> 
  <tr rowsep="1" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sem proteção</b> — Nenhuma ativação de proteção de saída é imposta para saídas analógicas e digitais. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
  <tr rowsep="0" class="- topic/row "> 
   <td colname="1" class="- topic/entry "> <p class="- topic/p "><b class="+ topic/ph hi-d/b ">Sem reprodução</b>  — Não permita a reprodução em um dispositivo externo para saídas analógicas e digitais. </p> </td> 
   <td colname="2" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
   <td colname="3" class="- topic/entry "> <p class="- topic/p ">SIM </p> </td> 
  </tr> 
 </tbody> 
</table>

>[!NOTE]
>
>Embora essas regras sejam aplicadas de forma consistente em todas as plataformas, atualmente, só é possível ativar a proteção de saída com segurança nas plataformas Windows. Em outras plataformas (como Macintosh e Linux) não há funções de sistema operacional de suporte disponíveis para aplicativos de terceiros.

Exemplo de caso de uso: Alguns conteúdos podem impor controles de proteção de saída, e o nível de proteção pode ser definido pelo distribuidor de conteúdo. Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada em um Macintosh, o cliente não reproduzirá conteúdo em dispositivos externos. No entanto, o conteúdo será reproduzido em monitores internos.

Se &quot;Obrigatório&quot; for especificado e a reprodução for tentada no Linux, o cliente não reproduzirá conteúdo em nenhum dispositivo porque não é possível diferenciar entre dispositivos internos e externos.

Se você especificar &quot;Usar se disponível&quot;, a proteção de saída será ativada quando possível. Por exemplo, em máquinas do Windows que oferecem suporte ao Certified Output Protection Protocol (COPP), o conteúdo é transmitido com proteção de saída para um monitor externo. Esse exemplo é conhecido às vezes como &quot;controle de saída selecionável&quot;.
