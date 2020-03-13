---
description: O TVSDK oferece suporte a anúncios de banners companheiros, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o término do anúncio linear. Seu aplicativo é responsável por exibir os banners associados que são fornecidos com um anúncio linear.
seo-description: O TVSDK oferece suporte a anúncios de banners companheiros, que são anúncios que acompanham um anúncio linear e geralmente permanecem na página após o término do anúncio linear. Seu aplicativo é responsável por exibir os banners associados que são fornecidos com um anúncio linear.
seo-title: Anúncios em banner do Companion
title: Anúncios em banner do Companion
uuid: 522578ff-1f09-48f1-91f7-f074cfd34064
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

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

O conteúdo de um PTAdAsset descreve um banner associado.

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

A `PTMediaPlayerAdStartedNotification` notificação retorna uma `PTAd` instância que contém uma `companionAssets` propriedade (matriz de `PtAdAsset`).
Cada um `PtAdAsset` fornece informações sobre como exibir o ativo.

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"><b>Informações disponíveis</b></th> 
   <th colname="col2" class="entry"><b>Descrição</b></th> 
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
     <li id="li_76B945007CE842158B5125422765E0B2">estático: Os dados são um staticURL que é um URL direto para uma imagem. </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> data </td> 
   <td colname="col2"> Os dados do tipo especificado por <span class="codeph">resourceType</span> para este banner complementar. </td> 
  </tr> 
 </tbody> 
</table>

## Exibir anúncios em banners {#display-banner-ads}

Para exibir anúncios em banners, é necessário criar instâncias de banner e permitir que o TVSDK escute eventos relacionados a anúncios.

O TVSDK fornece uma lista de anúncios de banner associados a um anúncio linear por meio do evento de `PTMediaPlayerAdPlayStartedNotification` notificação.

Os manifestos podem especificar anúncios de banner companheiro:

* Um trecho HTML
* O URL de uma página do iFrame
* O URL de uma imagem estática ou de um arquivo Adobe Flash SWF

Para cada anúncio complementar, o TVSDK indica quais tipos estão disponíveis para seu aplicativo.

1. Crie uma `PTAdBannerView` instância para cada slot de anúncio associado na sua página.

       Verifique se as seguintes informações foram fornecidas:
   
   * Para impedir a recuperação de anúncios complementares de tamanhos diferentes, uma instância de banner que especifica a largura e a altura.
   * Tamanhos de banner padrão.

1. Adicione um observador para o `PTMediaPlayerAdStartedNotification` que faz o seguinte:
   1. Limpa os anúncios existentes na instância do banner.
   1. Obtém a lista de anúncios complementares `Ad.getCompanionAssets``PTAd.companionAssets`.
   1. Se a lista de anúncios complementares não estiver vazia, passe o mouse sobre a lista para ver as instâncias de banner.

      Cada instância do banner ( a `PTAdAsset`) contém informações, como largura, altura, tipo de recurso (html, iframe ou estático) e dados necessários para exibir o banner complementar.
   1. Se um anúncio de vídeo não tiver anúncios complementares reservados, a lista de ativos complementares não conterá dados para esse anúncio de vídeo.

      Para mostrar um anúncio de exibição independente, adicione a lógica ao script para executar uma tag de anúncio de exibição DFP normal (DoubleClick for Publishers) na instância apropriada do banner.
   1. Envia as informações do banner para uma função na sua página que exibe os banners em um local apropriado.

      Geralmente, isso é uma `div`função e sua função usa o `div ID` para exibir o banner. Por exemplo:

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
