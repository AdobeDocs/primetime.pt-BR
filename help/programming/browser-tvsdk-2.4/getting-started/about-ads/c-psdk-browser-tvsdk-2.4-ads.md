---
description: Quando o conteúdo está sendo reproduzido, o TVSDK do navegador pode exibir anúncios e transmitir informações sobre anúncios ao criar o objeto MediaResource.
seo-description: Quando o conteúdo está sendo reproduzido, o TVSDK do navegador pode exibir anúncios e transmitir informações sobre anúncios ao criar o objeto MediaResource.
seo-title: Anúncios
title: Anúncios
uuid: 9a5e8c83-18ce-41e8-9cb1-fdc9da903faf
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 0%

---


# Visão geral {#ads-overview}

Quando o conteúdo está sendo reproduzido, o TVSDK do navegador pode exibir anúncios e transmitir informações sobre anúncios ao criar o objeto MediaResource.

Opcionalmente, você pode chamar a função `prepareToPlay` depois de receber `AdobePSDK.MediaPlayerStatus.INITIALIZED`.

```js
function onStatusChange (event) { 
   switch (event.status) { 
     case AdobePSDK.MediaPlayerStatus.INITIALIZED: 
        player.prepareToPlay(AdobePSDK.MediaPlayer.LIVE_POINT); 
        break; 
     case AdobePSDK.MediaPlayerStatus.PREPARED: 
        player.play(); 
        break; 
   } 
} 
 
var auditudeSettings     = new AdobePSDK.AuditudeSettings(); 
auditudeSettings.domain  = "sample_auditude_domain"; 
auditudeSettings.mediaId = "sample_media_id"; 
auditudeSettings.zoneId  = "sample_zone_id"; 
 
// event handler 
player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange); 
 
var mediaResource = new AdobePSDK.MediaResource(resourceUrl, resourceType, auditudeSettings, false);
```

O TVSDK do navegador também fornece os seguintes eventos específicos para anúncios que você pode usar nos manipuladores de eventos para impedir que o conteúdo seja encaminhado rapidamente quando os anúncios estiverem sendo reproduzidos:

* `AdobePSDK.PSDKEventType.AD_BREAK_STARTED`
* `AdobePSDK.PSDKEventType.AD_BREAK_COMPLETED`
* `AdobePSDK.PSDKEventType.AD_STARTED`
* `AdobePSDK.PSDKEventType.AD_COMPLETED`

Para ver isso funcionando na Estrutura da interface do usuário, especifique as configurações do anúncio na configuração da seguinte maneira:

```js
// Using UI Framework 
var playerWrapper = ptp.videoPlayer('.videoDiv', { 
    player: { 
        mediaResource: { 
 
            resourceUrl:'Specify Resource Url', 
 
            auditudeSettings: { 
                validMimeTypes: ["application/x-mpeURL"], 
                domain: "Sample_auditude_domain", 
                mediaId:"sample_media_id", 
                zoneID:"sample_zone_id", 
                creativeRepackagingEnabled:true 
            } 
        } 
    } 
}; 
```

Para obter mais informações sobre os `AuditudeSettings` necessários, consulte [Metadados de inserção de anúncio](../../ad-insertion/ad-insertion-metadata/c-psdk-browser-tvsdk-2.4-ad-insertion-metadata.md).
