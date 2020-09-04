---
description: O conteúdo de um AdBannerAsset descreve um banner associado.
seo-description: O conteúdo de um AdBannerAsset descreve um banner associado.
seo-title: Dados de banner associado
title: Dados de banner associado
uuid: b2c709da-9d19-49d1-8116-9c947371b77c
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# Dados de banner associado{#companion-banner-data}

O conteúdo de um AdBannerAsset descreve um banner associado.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

O `AdobePSDK.PSDKEventType.AD_STARTED` evento retorna uma `Ad` instância que contém uma `companionAssets` propriedade ( `Array<AdBannerAsset>`).
Cada um `AdBannerAsset` fornece informações sobre como exibir o ativo.

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
   <td colname="col2"> <p>Às vezes, o banner complementar também pode ter um staticURL que é um URL direto para a imagem. </p> <p>Se você não quiser usar html ou iframe, poderá usar um URL direto para uma imagem. Nesse caso, você pode usar o staticURL para exibir o banner. </p> <p>Importante:  Você deve verificar se o URL estático é uma string válida, pois essa propriedade pode não estar sempre disponível. </p> </td> 
  </tr> 
 </tbody> 
</table>

