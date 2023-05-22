---
description: O reprodutor TVSDK envia eventos para exibir o status de carregamento do anúncio personalizado ou para ignorar um anúncio que está demorando muito para ser carregado ou que contém erros. Esses eventos são definidos em events.CustomAdEvents.
title: Eventos de publicidade personalizados
exl-id: 44f32584-7f6c-4071-82b6-9cc9584418ee
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# Eventos de publicidade personalizados{#custom-ad-events}

O reprodutor TVSDK envia eventos para exibir o status de carregamento do anúncio personalizado ou para ignorar um anúncio que está demorando muito para ser carregado ou que contém erros. Esses eventos são definidos em events.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Evento </th> 
   <th colname="col2" class="entry"> Definição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> O número de vezes que o visualizador clicou em um anúncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> Ocorreu um erro com o anúncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded </span> </td> 
   <td colname="col2"> O anúncio personalizado foi carregado.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> O anúncio personalizado está sendo carregado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused </span> </td> 
   <td colname="col2"> O anúncio personalizado foi pausado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> O anúncio personalizado continua sendo reproduzido após uma pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying </span> </td> 
   <td colname="col2"> O anúncio personalizado está sendo reproduzido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>O player de anúncio personalizado notifica o player de TVSDK sobre o progresso do anúncio personalizado. &amp;nbsp; </p> <p>A variável <span class="codeph"> currentTime </span> e <span class="codeph"> totalTime </span> do anúncio são transmitidos com esse evento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> O anúncio personalizado começou a ser reproduzido e é exibido ao visualizador.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> O anúncio personalizado terminou de ser reproduzido. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->
