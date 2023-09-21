---
description: Em dispositivos que oferecem suporte à aceleração GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar o vídeo diretamente no hardware do dispositivo.
title: Requisitos mínimos do StageVideo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Requisitos mínimos do StageVideo{#stagevideo-minimum-requirements}

Em dispositivos que oferecem suporte à aceleração GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar o vídeo diretamente no hardware do dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Uma combinação de diferentes fatores determina quando e como você pode usar o `StageVideo`. A tabela a seguir apresenta um instantâneo de alguns dos requisitos e restrições associados ao uso do StageVideo. Esses requisitos e restrições estão sujeitos a alterações.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Platform </th> 
   <th colname="col2" class="entry"> SO Windows e Mac </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash player </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Pelo menos o Flash 10.1 ou posterior </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Para o recurso de fallback para software, Flash 15 e posterior </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Navegadores e <span class="codeph"> wmode</span> configurações </td> 
   <td colname="col2"> <p><b>No Flash 15</b>, definir <span class="codeph"> wmode=opaque</span> portanto, você pode usar as sobreposições de HTML. </p> <p>Os seguintes navegadores não suportam aceleração de hardware no momento: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox no Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome anterior a 26 e qualquer versão do Chrome no Windows XP e Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (todas as versões) </li> 
     </ul>Outras combinações de navegador/SO podem impedir o acesso à aceleração de hardware. Nesses cenários, <span class="codeph"> StageVideo</span> recorre a software com impacto negativo no desempenho. </p> <p><b>No Flash 14 e anterior</b>, se o navegador não oferecer suporte à aceleração de hardware, o reprodutor do Flash poderá ser renderizado diretamente na GPU, mas definir <span class="codeph"> wmode=direct</span> para ativar essa renderização. <p>Dica: os drivers de GPU anteriores a 2009 podem precisar ser atualizados, pois esses drivers podem não ter suporte para aceleração de hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Objeto NetStream </td> 
   <td colname="col2">A variável <span class="codeph"> StageVideoEvent.RENDER_STATE</span> evento não é despachado a menos que você anexe um <span class="codeph"> NetStream</span> objeto para o <span class="codeph"> StageVideo</span> objeto. </td> 
  </tr> 
 </tbody> 
</table>
