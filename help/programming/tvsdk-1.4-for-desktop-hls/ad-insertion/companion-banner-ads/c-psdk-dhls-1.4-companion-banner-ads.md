---
description: O TVSDK oferece suporte a anúncios de banners companheiros, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o término do anúncio linear. Seu aplicativo é responsável por exibir os banners associados que são fornecidos com um anúncio linear.
seo-description: O TVSDK oferece suporte a anúncios de banners companheiros, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o término do anúncio linear. Seu aplicativo é responsável por exibir os banners associados que são fornecidos com um anúncio linear.
seo-title: Anúncios em banner do Companion
title: Anúncios em banner do Companion
uuid: 388a1683-342c-4f3b-97c8-cfcb6c5cfee1
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40

---


# Anúncios em banner do Companion {#companion-banner-ads}

O TVSDK oferece suporte a anúncios de banners companheiros, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o término do anúncio linear. Seu aplicativo é responsável por exibir os banners associados que são fornecidos com um anúncio linear.

Ao exibir anúncios complementares, siga estas recomendações:

* Tente apresentar tantos anúncios de banner companion de um anúncio de vídeo quantos couberem no layout do player.
* Apresente um banner complementar somente se você tiver um local que corresponda exatamente à altura e largura especificadas.

   >[!TIP]
   >
   >Não redimensione o banner.

* Apresente os banners companheiros assim que possível após o início do anúncio.
* Não sobreponha o contêiner principal de anúncio/vídeo com banners associados.
* Continue exibindo os banners de companheiro após o término do anúncio.

   O padrão é exibir cada banner complementar até que você tenha uma substituição para esse banner.

## Dados de banner associado {#companion-banner-data}

O conteúdo de um AdBannerAsset descreve um banner associado.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

O `AdPlaybackEvent.AD_STARTED` evento retorna uma `Ad` instância que contém uma `companionAssets` propriedade ( `Vector.<AdAsset>`).
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
   <td colname="col1"> dados do banner </td> 
   <td colname="col2"> Os dados do tipo especificado por <span class="codeph"> resourceType</span> para este banner complementar. </td> 
  </tr> 
  <tr> 
   <td colname="col1"> URL estático </td> 
   <td colname="col2"> <p>Às vezes, o banner complementar também tem um URL estático que é um URL direto para a imagem ou para um <span class="filepath"> .swf</span> (banner flash). </p> <p>Se você não quiser usar html ou iframe, poderá usar um URL direto para uma imagem ou swf para exibir o banner no estágio Flash. Nesse caso, você pode usar o staticURL para exibir o banner. </p> <p>Importante:  Você deve verificar se o URL estático é uma string válida, pois essa propriedade pode não estar sempre disponível. </p> </td> 
  </tr> 
 </tbody> 
</table>

## Exibir anúncios em banners {#display-banner-ads}

Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner associados a um anúncio linear por meio do evento `AdPlaybackEvent.AD_STARTED` event.

Os manifestos podem especificar anúncios de banner companheiro:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou de um arquivo Adobe Flash SWF

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

Adicione um ouvinte para o `AdPlaybackEvent.AD_STARTED` evento que faça o seguinte:

1. Limpa os anúncios existentes na instância do banner.

1. Obtém a lista de anúncios complementares de `Ad.companionAssets`.

1. Se a lista de anúncios complementares não estiver vazia, passe o mouse sobre a lista para ver as instâncias de banner.

   Cada instância do banner ( an `AdBannerAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.

1. Se um anúncio de vídeo não tiver anúncios complementares reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.

   Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP normal (DoubleClick for Publishers) na instância apropriada do banner.

1. Envia as informações do banner para uma função na sua página, geralmente JavaScript, usando `ExternalInterface`, que exibe os banners em um local apropriado.

   Geralmente, isso é uma `div`função e sua função usa o `div ID` para exibir o banner. Por exemplo:

   Adicione o ouvinte de eventos:

   ```js
   _player.addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted);
   ```

   Implemente o manipulador do listener:

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
