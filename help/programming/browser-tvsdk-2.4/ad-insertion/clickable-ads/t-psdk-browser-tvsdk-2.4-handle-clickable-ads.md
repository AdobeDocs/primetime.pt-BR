---
description: O MediaPlayer fornece uma função notifyClick() que envia eventos relacionados a anúncios quando um anúncio clicável está sendo reproduzido. Esses eventos fornecem informações de anúncios e ad break que o aplicativo pode usar para fornecer a funcionalidade de click-through.
title: Lidar com anúncios clicáveis
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Lidar com anúncios clicáveis {#handle-clickable-ads}

O MediaPlayer fornece uma função notifyClick() que envia eventos relacionados a anúncios quando um anúncio clicável está sendo reproduzido. Esses eventos fornecem informações de anúncios e ad break que o aplicativo pode usar para fornecer a funcionalidade de click-through.

O MediaPlayer aciona os seguintes eventos quando um anúncio clicável é reproduzido:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

A variável `AdClickedEvent` contém as informações necessárias para processar a função click-through.

1. Forneça um controle no player para que os usuários cliquem em anúncios clicáveis.

   Pode ser um botão ou qualquer outro elemento para capturar o clique do usuário.
1. Adicione um ouvinte de eventos para o evento de clique do usuário.

   Por exemplo:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Adicione um manipulador para o evento de cliques do usuário.

   Esse manipulador precisa avisar o MediaPlayer para acionar o `AdClicked` evento.

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

1. Adicione ouvintes de eventos para as notificações de início de anúncio do MediaPlayer, anúncios clicados e anúncios concluídos.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Adicionar manipuladores de eventos.
a. Manipule o evento de início de anúncio.
Isso pode fazer qualquer coisa, como configurar a interface do usuário para o usuário.

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

   b. Manipule o evento de anúncio clicado.
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
