---
description: O TVSDK é compatível com a exibição de anúncios VPAID (Video Player-Ad Interface Definition) em ad break. A versão 1.0 do VPAID requer o Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.
title: Exibir anúncios VPAID lineares em um ad break
exl-id: 316a38ac-ec2d-498c-b441-304e2fa75993
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Exibir anúncios VPAID lineares em um ad break{#display-linear-vpaid-ads-in-an-ad-break}

O TVSDK é compatível com a exibição de anúncios VPAID (Video Player-Ad Interface Definition) em ad break. A versão 1.0 do VPAID requer o Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.

Para exibir anúncios VPAID corretamente, é necessário fornecer um contêiner de anúncio ( `AdContainerView`) no prazo de `MediaPlayerContext` instância.

Limitações para anúncios VPAID:

* Os anúncios VPAID não têm necessariamente uma duração predefinida, pois o anúncio pode ser interativo. Portanto, a duração do anúncio (definida pela resposta do servidor de anúncios) pode nem sempre corresponder exatamente à duração real do anúncio.
* Para anúncios VPAID 1.0, o TVSDK requer o Flash player 14.0.0.160 ou superior instalado no dispositivo. Para versões anteriores do reprodutor do Flash, esse recurso está desativado e os anúncios VPAID 1.0 são ignorados.

Para configurar um contêiner de anúncios para exibir anúncios VPAID (versão 1.0 ou 2.0) em um ad break:

1. Use o código de exemplo a seguir para configurar um contêiner de anúncios que possa mostrar anúncios VPAID.

   ```
   var context:MediaPlayerContext =  
     new MediaPlayerContext(_authorizedFeatureHelper.authorizedFeatures); 
   
   adContainer = new AdContainerView(); 
   adContainer.x = adContainer.y = 0; 
   adContainer.setSize(videoContainer.width, videoContainer.height); 
   addChild(adContainer); 
   
   context.adContainer = adContainer; 
   _player = new DefaultMediaPlayer(context);
   ```

1. Quando a visualização for redimensionada, redefina o tamanho no contêiner de anúncios.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Ao obter um evento de alteração de tela inteira e definir o novo tamanho no contêiner de anúncio, passe o estado de exibição do estágio da seguinte maneira para garantir que o reprodutor seja redimensionado corretamente:
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```
