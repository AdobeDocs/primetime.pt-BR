---
description: Em dispositivos que suportam a aceleração da GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo diretamente no hardware do dispositivo.
title: Requisitos mínimos do StageVideo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Requisitos mínimos do StageVideo{#stagevideo-minimum-requirements}

Em dispositivos que suportam a aceleração da GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo diretamente no hardware do dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Uma combinação de diferentes fatores determina quando e como você pode usar `StageVideo`. A tabela a seguir apresenta um resumo de alguns dos requisitos e restrições associados ao uso do StageVideo. Estes requisitos e restrições estão sujeitos a alterações.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Plataforma </th> 
   <th colname="col2" class="entry"> Windows e Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Reprodutor do Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Pelo menos Flash 10.1 ou posterior </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Para o recurso de fallback para software, Flash 15 e posterior </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Navegadores e configurações <span class="codeph"> wmode</span> </td> 
   <td colname="col2"> <p><b>No Flash 15</b>, defina  <span class="codeph"> wmode=</span> opaqueso para usar as sobreposições HTML. </p> <p>Os seguintes navegadores atualmente não suportam aceleração de hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox no Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome antes de 26 e qualquer versão do Chrome no Windows XP e Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (todas as versões) </li> 
     </ul>Outras combinações de navegador/SO podem impedir o acesso à aceleração de hardware. Nesses cenários, <span class="codeph"> StageVideo</span> retorna ao software com um impacto negativo no desempenho. </p> <p><b>No Flash 14 e anterior</b>, se o navegador não suportar aceleração de hardware, o reprodutor do Flash poderá renderizar diretamente para a GPU, mas definir  <span class="codeph"> wmode=</span> diretamente para habilitar essa renderização. <p>Dica:  Os drivers de GPU anteriores a 2009 podem precisar ser atualizados, pois esses drivers podem não ter suporte para aceleração de hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Objeto NetStream </td> 
   <td colname="col2">O evento <span class="codeph"> StageVideoEvent.RENDER_STATE</span> não é despachado a menos que você anexe um objeto <span class="codeph"> NetStream</span> ao objeto <span class="codeph"> StageVideo</span>. </td> 
  </tr> 
 </tbody> 
</table>

