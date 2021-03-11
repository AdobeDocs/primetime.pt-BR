---
description: O TVSDK fornece informações para que você possa agir com anúncios de click-through. À medida que você cria a interface do usuário do player, deve decidir como responder quando um usuário clica em um anúncio clicável.
title: Anúncios clicáveis
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Anúncios clicáveis {#clickable-ads}

O TVSDK fornece informações para que você possa agir com anúncios de click-through. À medida que você cria a interface do usuário do player, deve decidir como responder quando um usuário clica em um anúncio clicável.

Para TVSDK para Flash Runtime, somente anúncios lineares podem ser clicados.

## Responder cliques em anúncios {#respond-to-clicks-on-ads}

Quando um usuário clica em uma publicidade ou em um botão relacionado, seu aplicativo é responsável por responder. O TVSDK fornece informações sobre o URL de destino.

Este exemplo mostra uma maneira possível de gerenciar cliques de anúncios.

1. Cada vez que um anúncio é reproduzido, exiba um botão no reprodutor de mídia. Um usuário que clica no anúncio é redirecionado para o URL do anúncio. Esse botão faz parte do [!DNL ClickableAdsOverlay.xml].

   ```xml
      <?xml version="1.0"?> 
   <s:VGroup xmlns:fx="https://ns.adobe.com/mxml/2009"  
       xmlns:s="library://ns.adobe.com/flex/spark" percentWidth="100" horizontalAlign="center">     
           <fx:Declarations><fx:String id="text"/></fx:Declarations> 
           <s:Label text="{text}"  backgroundAlpha="0.75" backgroundColor="#DEDEDE"  
               color="#000000" paddingBottom="5" paddingRight="5" paddingLeft="5"  
               paddingTop="5"/> 
   </s:VGroup>
   ```

1. Inclua essa sobreposição na amostra do reprodutor de mídia, [!DNL psdkdemo.xml].

   ```xml
      <psdk:ClickableAdsOverlay id="clickableAdsOverlay"  
       visible="false"   top="10" right="0" left="0"  
       text="Click here for more information"   
       click="onAdsOverlayClicked()" 
   </psdk:ClickableAdsOverlay
   ```

1. Para tornar a exibição visível somente quando um anúncio está sendo reproduzido, acompanhe os eventos `onAdStart` e `onAdComplete` despachados por .

   ```
   _player.addEventListener(AdPlaybackEvent.AD_STARTED, onAdStarted); 
   _player.addEventListener(AdPlaybackEvent.AD_COMPLETED, onAdCompleted); 
   ```

   ```
      private function onAdStarted(event:AdPlaybackEvent):void { 
       var primaryAsset:AdAsset = event.ad.primaryAsset; 
       if (primaryAsset.adClick != null) { 
           clickableAdsOverlay.visible = true;  
       } 
   } 
   private function onAdCompleted(event:AdPlaybackEvent):void { 
       clickableAdsOverlay.visible = false; 
   }
   ```

1. Monitore as interações do usuário em anúncios clicáveis. Quando o usuário tocar ou clicar no botão, notifique o TVSDK com `notifyClick`.

   ```
   private function onAdsOverlayClicked():void {     
       _mediaPlayer.view.notifyClick(); 
   }
   ```

1. Analise o evento `AdclickEvent.AD_CLICK`.

   Se um anúncio estiver sendo reproduzido, o TVSDK despacha o evento `AdClickEvent.AD_CLICK`, do qual você pode recuperar o URL de click-through e as informações relacionadas.

   ```
      _player.addEventListener(AdClickEvent.AD_CLICK, onAdClick);
   ```

1. Pause o reprodutor de mídia ao direcionar o usuário para o URL do anúncio.

   ```
   private function onAdClick(event:AdClickEvent):void { 
       _logger.info("#onAdClick Ad clicked. Target url is {0}", event.adClick.url);  
       _player.pause(); 
       var adRequest:URLRequest = new URLRequest(event.adClick.url); 
       navigateToURL(adRequest, event.adClick.title); 
   }
   ```

1. Exiba o URL de click-through do anúncio e qualquer informação relacionada.

       Por exemplo, você pode exibi-lo de uma das seguintes maneiras:
   
   * Abra o URL de click-through em um navegador dentro do aplicativo.

      Em plataformas de desktop, a área de reprodução do anúncio de vídeo é normalmente usada para chamar URLs de click-through após cliques do usuário.
   * Redirecione o usuário para o navegador da Web móvel externo.

      Em dispositivos móveis, a área de reprodução do anúncio de vídeo é usada para outras funções, como ocultar e mostrar controles, pausar a reprodução, expandir para tela cheia e assim por diante. Portanto, em dispositivos móveis, uma visualização separada, como um botão patrocinador, é geralmente apresentada ao usuário como um meio de iniciar o URL de click-through.

1. Feche a janela do navegador em que as informações de click-through são exibidas e retome a reprodução do vídeo.
