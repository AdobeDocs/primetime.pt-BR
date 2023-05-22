---
description: O conteúdo de um AdAsset descreve um banner complementar.
title: Dados de banner de companhia
exl-id: 922577fd-bc58-4669-b051-fe54b197a5f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# Dados de banner de companhia {#companion-banner-data}

O conteúdo de um AdAsset descreve um banner complementar.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Each `AdAsset` O fornece informações sobre a exibição do ativo.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> Informações disponíveis </th> 
   <th colname="col2" class="entry"> Descrição </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> largura </td> 
   <td colname="col2"> Largura do banner complementar em pixels. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> altura </td> 
   <td colname="col2"> Altura do banner complementar em pixels. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">O tipo de recurso para este banner complementar: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Os dados estão no código HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: os dados são um URL de iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estático </td> 
   <td colname="col2"> <p>Às vezes, o banner complementar também tem um <span class="codeph"> staticURL</span> que é um URL direto para a imagem ou para um <span class="codeph"> .swf</span> (banner flash). </p> <p>Se não quiser usar html ou iframe, você poderá usar um URL direto para uma imagem ou swf para exibir o banner no estágio de Flash. Nesse caso, você pode usar a variável <span class="codeph"> staticURL</span> para exibir o banner. </p> <p>Importante: você deve verificar se o URL estático é uma string válida, pois essa propriedade nem sempre pode estar disponível. </p> </td> 
  </tr> 
 </tbody> 
</table>
