---
description: O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface de reprodutor de vídeo (VPAID) em um ad break. A versão 1.0 do VPAID requer o Flash, enquanto a versão 2.0 também funciona com o Browser TVSDK e o JavaScript.
title: Exibir anúncios VPAID lineares em um ad break
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Exibir anúncios VPAID lineares em um ad break{#display-linear-vpaid-ads-in-an-ad-break}

O TVSDK oferece suporte à exibição de anúncios lineares de Definição de interface de reprodutor de vídeo (VPAID) em um ad break. A versão 1.0 do VPAID requer o Flash, enquanto a versão 2.0 também funciona com o Browser TVSDK e o JavaScript.

Para exibir anúncios VPAID corretamente, você deve fornecer um contêiner de anúncio ( `AdContainerView`) na instância `MediaPlayerContext`.

Limitações para anúncios VPAID:

* Anúncios VPAID não têm necessariamente uma duração predefinida, visto que o anúncio pode ser interativo. Portanto, a duração do anúncio (definida pela resposta do servidor de anúncios) pode nem sempre corresponder exatamente à duração real do anúncio.
* Para anúncios VPAID 1.0, o TVSDK requer o player do Flash 14.0.0.160 ou superior instalado no dispositivo. Para versões anteriores do reprodutor do Flash, esse recurso é desativado e os anúncios VPAID 1.0 são ignorados.

Para configurar um contêiner de anúncio para exibir anúncios VPAID (versão 1.0 ou 2.0) em um ad break:

1. Use o código de exemplo a seguir para configurar um contêiner de anúncio que possa exibir anúncios VPAID.

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
   >Ao obter um evento de alteração de tela cheia e definir o novo tamanho no contêiner de anúncio, passe o estado de exibição do palco da seguinte maneira para garantir que o redimensionamento do reprodutor seja feito corretamente:
   >
   >
   ```
   >private function onFullScreenChange(event:FullScreenEvent):void { 
   >if (_adContainer) 
   >{ _adContainer.setSize(stage.stageWidth, stage.stageHeight, stage.displayState); } 
   >}
   >```

