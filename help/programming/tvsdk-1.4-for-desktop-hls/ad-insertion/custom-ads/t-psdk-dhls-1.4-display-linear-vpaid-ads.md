---
description: O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface do player de vídeo (VPAID) em uma pausa de anúncio. A versão 1.0 do VPAID requer o Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.
seo-description: O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface do player de vídeo (VPAID) em uma pausa de anúncio. A versão 1.0 do VPAID requer o Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.
seo-title: Exibir anúncios VPAID lineares em uma pausa de anúncio
title: Exibir anúncios VPAID lineares em uma pausa de anúncio
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Exibir anúncios VPAID lineares em uma pausa de anúncio{#display-linear-vpaid-ads-in-an-ad-break}

O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface do player de vídeo (VPAID) em uma pausa de anúncio. A versão 1.0 do VPAID requer o Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.

Para exibir anúncios VPAID corretamente, é necessário fornecer um contêiner de anúncio ( `AdContainerView`) na `MediaPlayerContext` instância.

Limitações para anúncios VPAID:

* Anúncios VPAID não têm necessariamente uma duração predefinida, visto que o anúncio pode ser interativo. Portanto, a duração do anúncio (definida pela resposta do servidor de anúncios) pode não corresponder sempre exatamente à duração real do anúncio.
* Para anúncios VPAID 1.0, o TVSDK requer o Flash player 14.0.0.160 ou superior instalado no dispositivo. Para versões anteriores do Flash player, esse recurso é desativado e os anúncios VPAID 1.0 são ignorados.

Para configurar um contêiner de anúncio para exibir anúncios VPAID (versão 1.0 ou 2.0) em uma quebra de anúncio:

1. Use o código de amostra a seguir para configurar um contêiner de anúncio que possa mostrar anúncios VPAID.

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

1. Quando a exibição for redimensionada, redefina o tamanho no contêiner de publicidade.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Quando você receber um evento de alteração de tela cheia e definir o novo tamanho no contêiner de publicidade, passe o estado de exibição do palco da seguinte forma para garantir que o player seja redimensionado corretamente:    >
   >
   >
   ```>
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```   >
   >



