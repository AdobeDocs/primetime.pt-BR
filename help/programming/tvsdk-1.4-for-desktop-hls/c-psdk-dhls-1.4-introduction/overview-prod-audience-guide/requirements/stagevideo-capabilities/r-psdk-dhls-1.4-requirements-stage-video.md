---
description: Em dispositivos que suportam aceleração de GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo diretamente no hardware do dispositivo.
seo-description: Em dispositivos que suportam aceleração de GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo diretamente no hardware do dispositivo.
seo-title: Requisitos mínimos de StageVideo
title: Requisitos mínimos de StageVideo
uuid: 8916dbac-33e0-4efd-8105-9ddbc85f0a3f
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---


# Requisitos mínimos do StageVideo{#stagevideo-minimum-requirements}

Em dispositivos que suportam aceleração de GPU (hardware), você pode usar um objeto flash.media.StageVideo para processar vídeo diretamente no hardware do dispositivo.

<!--<a id="section_64DDAA8DB215493E8A7CA6636819D350"></a>-->

Uma combinação de fatores diferentes determina quando e como você pode usar `StageVideo`. A tabela a seguir apresenta um instantâneo de alguns dos requisitos e restrições associados ao uso do StageVideo. Estes requisitos e restrições estão sujeitos a alterações.

<table id="table_882F4462A5AE47E28A60A39D112164A7"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Plataforma </th> 
   <th colname="col2" class="entry"> Windows e Mac OS </th> 
  </tr>
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> Flash </td> 
   <td colname="col2"> 
    <ul id="ul_s42_lm2_jp"> 
     <li id="li_308FA9EC206B437A9EE04C29F9480B73">Pelo menos Flash 10.1 ou posterior </li> 
     <li id="li_5898EDB0D12A43389076BCC7F4A27A0A">Para o recurso de fallback para software, Flash 15 e posterior </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">Navegadores e configurações <span class="codeph"> wmode</span> </td> 
   <td colname="col2"> <p><b>No Flash 15</b>, defina  <span class="codeph"> wmode=</span> opaqueso para usar sobreposições HTML. </p> <p>Os seguintes navegadores atualmente não suportam aceleração de hardware: 
     <ul id="ul_frv_ykf_jp"> 
      <li id="li_3D407A61FEE042A9B85A6EFACA6D7719">Mozilla Firefox no Microsoft Windows </li> 
      <li id="li_39B85AC352564DA8B86EA826638F1F4B">Google Chrome antes de 26 e qualquer versão do Chrome no Windows XP e Vista </li> 
      <li id="li_0042BA6070C849E6B7C4B4BF4333F712">Microsoft Internet Explorer (todas as versões) </li> 
     </ul>Outras combinações de navegador/SO podem impedir o acesso à aceleração de hardware. Nesses cenários, o <span class="codeph"> StageVideo</span> volta para o software com um impacto negativo no desempenho. </p> <p><b>No Flash 14 e anterior</b>, se o navegador não suportar aceleração de hardware, o player do Flash poderá renderizar diretamente na GPU, mas definir  <span class="codeph"> wmode=</span> directpara habilitar essa renderização. <p>Dica:  Drivers de GPU mais antigos que 2009 podem precisar ser atualizados, pois esses drivers podem não ter suporte para aceleração de hardware. </p> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> Objeto NetStream </td> 
   <td colname="col2">O evento <span class="codeph"> StageVideoEvent.RENDER_STATE</span> não é despachado a menos que você anexe um objeto <span class="codeph"> NetStream</span> ao objeto <span class="codeph"> StageVideo</span>. </td> 
  </tr> 
 </tbody> 
</table>

