---
description: O player do TVSDK despacha eventos para exibir o status de carregamento de anúncio personalizado ou para ignorar um anúncio que está demorando muito para carregar ou que apresenta erros. Esses eventos são definidos em eventos.CustomAdEvents.
seo-description: O player do TVSDK despacha eventos para exibir o status de carregamento de anúncio personalizado ou para ignorar um anúncio que está demorando muito para carregar ou que apresenta erros. Esses eventos são definidos em eventos.CustomAdEvents.
seo-title: Eventos de anúncio personalizados
title: Eventos de anúncio personalizados
uuid: 78e2ccf4-5943-4c60-84be-623182d9a300
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# Eventos de anúncio personalizados{#custom-ad-events}

O player do TVSDK despacha eventos para exibir o status de carregamento de anúncio personalizado ou para ignorar um anúncio que está demorando muito para carregar ou que apresenta erros. Esses eventos são definidos em eventos.CustomAdEvents.

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Evento </th> 
   <th colname="col2" class="entry"> Definição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru  </span> </td> 
   <td colname="col2"> O número de vezes que o visualizador clicou em um anúncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError  </span> </td> 
   <td colname="col2"> Ocorreu um erro com o anúncio personalizado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded  </span> </td> 
   <td colname="col2"> O anúncio personalizado foi carregado.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading  </span> </td> 
   <td colname="col2"> O anúncio personalizado está sendo carregado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused  </span> </td> 
   <td colname="col2"> O anúncio personalizado foi pausado. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed  </span> </td> 
   <td colname="col2"> O anúncio personalizado continuou sendo reproduzido após uma pausa. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying  </span> </td> 
   <td colname="col2"> O anúncio personalizado está sendo reproduzido. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress  </span> </td> 
   <td colname="col2"> <p>O player de publicidade personalizado notifica o player TVSDK sobre o progresso do anúncio personalizado. &amp;nbsp; </p> <p>As <span class="codeph"> currentTime </span> e <span class="codeph"> totalTime </span> do anúncio são transmitidas com este evento. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> O anúncio personalizado começou a ser reproduzido e é exibido ao visualizador.  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> A reprodução do anúncio personalizado terminou. </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

