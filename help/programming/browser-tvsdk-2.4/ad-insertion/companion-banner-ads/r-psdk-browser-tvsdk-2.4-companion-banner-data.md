---
description: O conteúdo de um AdBannerAsset descreve um banner complementar.
title: Dados de banner complementar
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---


# Dados do banner complementar{#companion-banner-data}

O conteúdo de um AdBannerAsset descreve um banner complementar.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

O evento `AdobePSDK.PSDKEventType.AD_STARTED` retorna uma instância `Ad` que contém uma propriedade `companionAssets` ( `Array<AdBannerAsset>`).
Cada `AdBannerAsset` fornece informações sobre como exibir o ativo.

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
     <li id="li_5F37E14472424F808C6094F42009E676">iframe: Os dados são um URL de iframe (src). </li> 
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">estático: Os dados são um URL de imagem estática (src). </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      dados do banner
    </pre> </td> 
   <td colname="col2"> Os dados do tipo especificado por <span class="codeph"> resourceType</span> para este banner complementar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estático </td> 
   <td colname="col2"> <p>Às vezes, o banner complementar também pode ter um URL estático que é um URL direto para a imagem. </p> <p>Se você não quiser usar html ou iframe, poderá usar um URL direto para uma imagem. Nesse caso, você pode usar a staticURL para exibir o banner. </p> <p>Importante:  Você deve verificar se o URL estático é uma string válida, pois essa propriedade pode nem sempre estar disponível. </p> </td> 
  </tr> 
 </tbody> 
</table>

