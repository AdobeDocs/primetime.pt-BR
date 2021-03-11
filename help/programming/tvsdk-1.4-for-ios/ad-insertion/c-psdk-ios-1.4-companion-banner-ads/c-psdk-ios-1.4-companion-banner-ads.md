---
description: O TVSDK suporta anúncios de banner complementar, que são anúncios que acompanham um anúncio linear e que geralmente permanecem na página depois que o anúncio linear termina. Seu aplicativo é responsável por exibir os banners complementares que são fornecidos com um anúncio linear.
title: Anúncios de banner complementares
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Anúncios de banner complementares {#companion-banner-ads}

O TVSDK suporta anúncios de banner complementar, que são anúncios que acompanham um anúncio linear e que geralmente permanecem na página depois que o anúncio linear termina. Seu aplicativo é responsável por exibir os banners complementares que são fornecidos com um anúncio linear.

Ao exibir anúncios complementares, siga estas recomendações:

* Tente apresentar o máximo possível de anúncios de banner complementares de um anúncio de vídeo que couberem no layout do player.
* Apresente um banner complementar somente se você tiver um local que corresponda exatamente à altura e largura especificadas.

   >[!TIP]
   >
   >Não redimensione o banner.

* Apresente os banners complementares assim que possível após o início do anúncio.
* Não sobreponha o contêiner principal de anúncio/vídeo com banners complementares.
* Continue exibindo banners complementares depois que o anúncio terminar.

   O padrão é exibir cada banner complementar até que você tenha uma substituição para esse banner.

## Dados do banner complementar {#companion-banner-data}

O conteúdo de um PTAdAsset descreve um banner complementar.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

A notificação `PTMediaPlayerAdStartedNotification` retorna uma instância `PTAd` que contém uma propriedade `companionAssets` (matriz de `PtAdAsset`).
Cada `PtAdAsset` fornece informações sobre como exibir o ativo.

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
     <li id="li_76B945007CE842158B5125422765E0B2">estático: Os dados são um staticURL que é um URL direto para uma imagem. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> dados </td> 
   <td colname="col2"> Os dados do tipo especificado por <span class="codeph"> resourceType</span> para este banner complementar. </td> 
  </tr> 
 </tbody> 
</table>

## Exibir anúncios de banner {#display-banner-ads}

Para exibir anúncios de banner, é necessário criar instâncias de banner e permitir que o TVSDK acompanhe eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner complementar associados a um anúncio linear por meio do evento de notificação `PTMediaPlayerAdPlayStartedNotification`.

Os manifestos podem especificar anúncios de banner complementar ao:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou um arquivo SWF de Flash Adobe

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

1. Crie uma instância `PTAdBannerView` para cada slot de anúncio complementar na página.

       Verifique se as seguintes informações foram fornecidas:
   
   * Para evitar a recuperação de anúncios complementares de tamanhos diferentes, uma instância de banner que especifica a largura e a altura.
   * Tamanhos de banner padrão.

1. Adicione um observador para o `PTMediaPlayerAdStartedNotification` que faz o seguinte:
   1. Apaga anúncios existentes na instância do banner.
   1. Obtém a lista de anúncios complementares de `Ad.getCompanionAssets` `PTAd.companionAssets`.
   1. Se a lista de anúncios complementares não estiver vazia, passe o mouse sobre a lista para as instâncias de banner.

      Cada instância de banner ( a `PTAdAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
   1. Se um anúncio de vídeo não tiver anúncios complementares reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.

      Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP normal (DoubleClick for Publishers) na instância apropriada do banner.
   1. Envia as informações do banner para uma função na página que exibe os banners em um local apropriado.

      Geralmente é um `div`, e sua função usa o `div ID` para exibir o banner. Por exemplo:

      ```
      - (void) onMediaPlayerAdPlayStarted:(NSNotification *) notification { 
          _currentAd  = [notification.userInfo  objectForKey:PTMediaPlayerAdKey];  
          if (_currentAd != nil) { 
              [self removeAllBanners]; // remove any existing PTAdBannerView views 
      
              // banners 
              if (_currentAd.companionAssets && _currentAd.companionAssets.count > 0) { 
                  PTAdAsset *bannerAsset = [_currentAd.companionAssets objectAtIndex:0]; 
      
                  PTAdBannerView *bannerView = [[PTAdBannerView alloc] initWithAsset:bannerAsset];  
                  bannerView.player = self.player; 
                  bannerView.delegate = self; 
      
                  bannerView.frame = CGRectMake(0.0, 0.0, bannerAsset.width, bannerAsset.height);  
                  [_adBannerView.bannerView addSubview:bannerView]; 
              } 
          } 
      }
      ```
