---
description: O MediaPlayer fornece uma função NotificationClick() que despacha eventos relacionados a anúncios quando um anúncio clicável está sendo reproduzido. Esses eventos fornecem informações de quebra de anúncios e anúncios que seu aplicativo pode usar para fornecer a funcionalidade de click-through.
seo-description: O MediaPlayer fornece uma função NotificationClick() que despacha eventos relacionados a anúncios quando um anúncio clicável está sendo reproduzido. Esses eventos fornecem informações de quebra de anúncios e anúncios que seu aplicativo pode usar para fornecer a funcionalidade de click-through.
seo-title: Manipular anúncios clicáveis
title: Manipular anúncios clicáveis
uuid: 5d3c9d36-60d7-4272-a523-7d1fe0e1615f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Manipular anúncios clicáveis {#handle-clickable-ads}

O MediaPlayer fornece uma função NotificationClick() que despacha eventos relacionados a anúncios quando um anúncio clicável está sendo reproduzido. Esses eventos fornecem informações de quebra de anúncios e anúncios que seu aplicativo pode usar para fornecer a funcionalidade de click-through.

O MediaPlayer aciona os seguintes eventos quando um anúncio clicável é reproduzido:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

O `AdClickedEvent` contém as informações necessárias para processar a função de click-through.

1. Forneça um controle no player para que os usuários cliquem em anúncios clicáveis.

   Pode ser um botão ou qualquer outro elemento para capturar o clique do usuário.
1. Adicione um ouvinte de eventos para o evento de cliques em anúncios do usuário.

   Por exemplo:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Adicione um manipulador para o evento de clique do usuário.

   Esse manipulador precisa solicitar que o MediaPlayer acione o `AdClicked` evento.

   ```
   onAdClick = function (event) { 
       // Get a reference to your player 
       var player = getPlayer(); 
       if (player) { 
           // Call the MediaPlayer's notifyClick function 
           // which gets MediaPlayer to fire AdClicked 
           player.notifyClick(); 
       } 
   } 
   ```

1. Adicione ouvintes de eventos para o início do anúncio do MediaPlayer, o clique do anúncio e as notificações concluídas do anúncio.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Adicione manipuladores de eventos.
a. Manipule o evento de início do anúncio.
Isso pode fazer qualquer coisa, como configurar a interface do usuário.

   ```
   onAdStarted = function (event) { 
       if (clickAddButton && event && event.ad) { 
           var adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           if (adClick && adClick.isValid) { 
               // Do some initial processing  
               // when the ad starts, prior 
               // to the user's click. 
           } 
       } 
   }
   ```

   b. Manipule o evento clicado no anúncio.
Neste exemplo, obtemos informações de anúncios do evento e abrimos uma nova janela do navegador usando essas informações:

   ```
   onAdClickedEvent = function (event) { 
       if (event && event.ad) { 
           var adClick = event.adClick; 
           if (!(adClick && adClick.isValid)) { 
               adClick = event.ad.primaryAsset && event.ad.primaryAsset.adClick; 
           } 
           if (adClick && adClick.isValid) 
           { 
               // Do something with the currently playing ad 
               window.open(adClick.url); 
           } 
       } 
   }
   ```

   c. Manipule o evento de anúncio concluído.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
