---
description: O MediaPlayer fornece uma função notifyClick() que despacha eventos relacionados a anúncios quando um anúncio clicável é reproduzido. Esses eventos fornecem informações de ad break e ad break que seu aplicativo pode usar para fornecer funcionalidade de click-through.
title: Gerenciar anúncios clicáveis
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---


# Gerenciar anúncios clicáveis {#handle-clickable-ads}

O MediaPlayer fornece uma função notifyClick() que despacha eventos relacionados a anúncios quando um anúncio clicável é reproduzido. Esses eventos fornecem informações de ad break e ad break que seu aplicativo pode usar para fornecer funcionalidade de click-through.

O MediaPlayer aciona os seguintes eventos quando um anúncio clicável é reproduzido:

* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_CLICKED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

O `AdClickedEvent` contém as informações necessárias para processar a função de click-through.

1. Forneça um controle no player para que os usuários cliquem em anúncios clicáveis.

   Pode ser um botão ou qualquer outro elemento para capturar o clique do usuário.
1. Adicione um ouvinte de evento para o evento de clique de anúncio do usuário.

   Por exemplo:

   ```
   document.getElementById([ 
   <i>your_click_control_id</i>]).addEventListener("click", onAdClick);
   ```

1. Adicione um manipulador para o evento de clique do usuário.

   Esse manipulador precisa solicitar que o MediaPlayer acione o evento `AdClicked`.

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

1. Adicione ouvintes de eventos para o início do anúncio do MediaPlayer, o anúncio clicado e as notificações concluídas do anúncio.

   ```
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_STARTED, onAdStarted); 
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_COMPLETED, onAdCompleted);
   
    <i>your_player</i>().addEventListener(AdobePSDK.PSDKEventType.AD_CLICKED, onAdClickedEvent);
   ```

1. Adicione manipuladores de evento.
a. Manipule o evento de início do anúncio.
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
Neste exemplo, obtemos informações de anúncio do evento e abrimos uma nova janela do navegador usando essas informações:

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

   c. Lide com o evento de anúncio concluído.

   ```
   onAdCompleted = function (event) { 
       if (clickAddButton) { 
           clickAddButton.setAttribute('hidden', 'true'); 
       } 
   }
   ```
