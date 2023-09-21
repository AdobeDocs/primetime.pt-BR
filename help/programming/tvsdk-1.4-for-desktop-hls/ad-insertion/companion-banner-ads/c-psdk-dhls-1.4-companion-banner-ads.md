---
description: O TVSDK é compatível com anúncios de banner complementares, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o fim do anúncio linear. Seu aplicativo é responsável por exibir os banners de companhia que são fornecidos com um anúncio linear.
title: Anúncios de banner de companhia
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Anúncios de banner de companhia {#companion-banner-ads}

O TVSDK é compatível com anúncios de banner complementares, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o fim do anúncio linear. Seu aplicativo é responsável por exibir os banners de companhia que são fornecidos com um anúncio linear.

Ao exibir anúncios complementares, siga estas recomendações:

* Tente apresentar quantos anúncios de banner complementares de um anúncio de vídeo couberem no layout do reprodutor.
* Apresente um banner complementar somente se você tiver um local que corresponda exatamente à altura e largura especificadas.

  >[!TIP]
  >
  >Não redimensione o banner.

* Apresente os banner(s) complementar(es) o mais rápido possível após o início do anúncio.
* Não sobreponha o container principal de anúncios/vídeos com banners complementares.
* Continue a exibir os banners companheiros após o fim do anúncio.

  O padrão é exibir cada banner complementar até que você tenha uma substituição para esse banner.

## Dados de banner de companhia {#companion-banner-data}

O conteúdo de um AdBannerAsset descreve um banner complementar.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

A variável `AdPlaybackEvent.AD_STARTED` evento retorna um `Ad` instância que contém um `companionAssets` propriedade ( `Vector.<AdAsset>`).
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
   <td colname="col1"> dados do banner </td> 
   <td colname="col2"> Os dados do tipo especificado por <span class="codeph"> resourceType</span> para este banner complementar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estático </td> 
   <td colname="col2"> <p>Às vezes, o banner complementar também tem um URL estático que é um URL direto para a imagem ou para um <span class="filepath"> .swf</span> (banner flash). </p> <p>Se não quiser usar html ou iframe, você poderá usar um URL direto para uma imagem ou swf para exibir o banner no estágio de Flash. Nesse caso, você pode usar o staticURL para exibir o banner. </p> <p>Importante: você deve verificar se o URL estático é uma string válida, pois essa propriedade nem sempre pode estar disponível. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exibir anúncios de banner {#display-banner-ads}

Para exibir anúncios de banner, você precisa criar instâncias de banner e permitir que o TVSDK acompanhe eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner complementares associados a um anúncio linear por meio do `AdPlaybackEvent.AD_STARTED` evento.

Os manifestos podem especificar anúncios de banner complementares por:

* Um trecho de HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou de um arquivo SWF de Adobe Flash

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

Adicione um ouvinte para o `AdPlaybackEvent.AD_STARTED` evento que faz o seguinte:

1. Limpa os anúncios existentes na instância do banner.

1. Obtém a lista de anúncios complementares de `Ad.companionAssets`.

1. Se a lista de anúncios complementares não estiver vazia, repita sobre a lista para instâncias de banner.

   Cada instância do banner ( uma `AdBannerAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.

1. Se um anúncio de vídeo não tiver anúncios complementares reservados com ele, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.

   Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP (DoubleClick for Publishers) normal na instância de banner apropriada.

1. Envia as informações do banner para uma função na sua página, geralmente JavaScript, usando `ExternalInterface`, que exibe os banners em um local apropriado.

   Isso geralmente é um `div`, e sua função usa o `div ID` para exibir o banner. Por exemplo:

   Adicione o ouvinte de eventos:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implemente o manipulador do ouvinte:

   ```js
   private function onAdStarted(event:AdPlaybackEvent):void { 
       // check if there are any companion banner 
       if (event.ad && event.ad.companionAssets  
                    && event.ad.companionAssets.length > 0) { 
           for each (var banner:AdBannerAsset in event.ad.companionAssets) { 
               if (ExternalInterface.available) { 
                   //-- call the java script that will handle the banner display. 
                   ExternalInterface.call('addBanner', banner.resourceType,  
                       banner.width, banner.height, banner.bannerData); 
               } 
           } 
       }  
       //...        
   }
   ```

   Exemplo de JavaScript para lidar com a exibição:

   ```js
   function addBanner(resourceType, width, height, data) { 
       console.log(resourceType + "," +  width + "," +  height); 
   
   //Assume an html element on the page with id like 'banner300x250' 
       var bannerDiv = document.getElementById('banner' + width +  
           'x' + height);  
       if (bannerDiv != null) { 
           if (resourceType == "html") { // for html resource 
               bannerDiv.innerHTML = data; 
           } 
           else if (resourceType == "iframe") { // for iframe resource 
               bannerDiv.innerHTML = "<iframe src='" + data +  
                   "' width='100%' height='100%'></iframe>"; 
           } 
       } 
   }
   ```
