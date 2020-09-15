---
description: O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface do player de vídeo (VPAID) em uma pausa de anúncio. A versão 1.0 do VPAID requer Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.
seo-description: O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface do player de vídeo (VPAID) em uma pausa de anúncio. A versão 1.0 do VPAID requer Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.
seo-title: Exibir anúncios VPAID lineares em uma pausa de anúncio
title: Exibir anúncios VPAID lineares em uma pausa de anúncio
uuid: 1f3a5426-79f5-49a1-a913-923708c09ade
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Exibir anúncios VPAID lineares em uma pausa de anúncio{#display-linear-vpaid-ads-in-an-ad-break}

O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface do player de vídeo (VPAID) em uma pausa de anúncio. A versão 1.0 do VPAID requer Flash, enquanto a versão 2.0 também funciona com o TVSDK do navegador e o JavaScript.

Para exibir anúncios VPAID corretamente, é necessário fornecer um container de anúncio ( `AdContainerView`) na `MediaPlayerContext` instância.

Limitações para anúncios VPAID:

* Anúncios VPAID não têm necessariamente uma duração predefinida, visto que o anúncio pode ser interativo. Portanto, a duração do anúncio (definida pela resposta do servidor de anúncios) pode não corresponder sempre exatamente à duração real do anúncio.
* Para anúncios VPAID 1.0, o TVSDK exige o player de Flash 14.0.0.160 ou superior instalado no dispositivo. Para versões anteriores do player de Flash, esse recurso é desativado e os anúncios VPAID 1.0 são ignorados.

Para configurar um container de anúncio para exibir anúncios VPAID (versão 1.0 ou 2.0) em uma quebra de anúncio:

1. Use o seguinte código de exemplo para configurar um container de anúncio que possa mostrar anúncios VPAID.

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

1. Quando a visualização for redimensionada, redefina o tamanho no container do anúncio.

   ```
   adContainer.setSize(stage.stageWidth, stage.stageHeight);
   ```

   >[!NOTE]
   >
   >Ao obter um evento de alteração em tela cheia e definir o novo tamanho no container do anúncio, passe o estado de exibição do palco da seguinte maneira para garantir que o player seja redimensionado corretamente:
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

