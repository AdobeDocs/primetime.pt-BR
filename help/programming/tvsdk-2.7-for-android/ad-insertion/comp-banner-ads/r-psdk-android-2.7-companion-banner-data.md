---
description: O conteúdo de um AdAsset descreve um banner complementar.
seo-description: O conteúdo de um AdAsset descreve um banner complementar.
seo-title: Dados de banner associado
title: Dados de banner associado
uuid: 4a5d78e1-5abe-45a8-b50f-14f73fdcc879
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Dados de banner associado {#companion-banner-data}

O conteúdo de um AdAsset descreve um banner complementar.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

Cada um `AdAsset` fornece informações sobre como exibir o ativo.

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
   <td colname="col2"> Altura do banner companheiro em pixels. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> tipo de recurso </td> 
   <td colname="col2">O tipo de recurso para este banner complementar: 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html: Os dados estão no código HTML. </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Os dados são um URL iframe (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estático </td> 
   <td colname="col2"> <p>Às vezes, o banner complementar também tem um URL <span class="codeph"></span> estático que é um URL direto para a imagem ou para um <span class="codeph"> .swf</span> (banner flash). </p> <p>Se você não quiser usar html ou iframe, poderá usar um URL direto para uma imagem ou swf para exibir o banner no estágio Flash. Nesse caso, você pode usar o <span class="codeph"> URL</span> estático para exibir o banner. </p> <p>Importante:  Você deve verificar se o URL estático é uma string válida, pois essa propriedade pode não estar sempre disponível. </p> </td> 
  </tr> 
 </tbody> 
</table>

