---
description: Você pode concluir fluxos de trabalho específicos do Digital Rights Management (DRM).
title: Digital Rights Management
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Digital Rights Management {#digital-rights-management}

Você pode concluir fluxos de trabalho específicos do Digital Rights Management (DRM).

Você pode ouvir o `AdobePSDK.DRMMetadataInfoEvent` evento para lidar com fluxos de trabalho DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Adicionar Digital Rights Management {#add-digital-rights-management}

1. Adicione o `DRMMetadataInfoAvailableEvent` para obter a `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implementar o `onDRMMetadataInfoAvailable` acima da linha na etapa 1.

   ```js
   var onDRMMetadataInfoAvaialble = function(event) { 
    var drmMetadataInfo = event.drmMetadataInfo; 
    var drmMetadata = null; 
   
    if(drmMetadataInfo) { 
     drmMetadata = drmMetadataInfo.drmMetadata; 
    } 
   
    drmManager.acquireLicense(drmMetadata, null, null); 
   };
   ```

1. Crie o DRMManager no método setupVideo.

   ```js
   var drmManager = player.drmManager;
   ```

1. Crie os dados de proteção para Widevine e PlayReady copiando o exemplo a seguir:

   ```js
   var protectionData = { 
     "com.widevine.alpha":{ 
       "serverURL":"https://wv.service.expressplay.com/hms/wv/rights/? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]"  
     }, 
   
     "com.microsoft.playready":{ 
       "serverURL":"https://pr.test.expressplay.com/playready/RightsManager.asmx? 
                    ExpressPlayToken=[YOUR_EXPRESSPLAY_TOKEN]", 
         "httpRequestHeaders":{ 
       } 
     } 
   };
   ```

1. Adicione os dados de proteção ao drmManager.

   ```js
   drmManager.setProtectionData(protectionData);
   ```

1. Altere o URL do recurso para um fluxo de teste DASH.

   >[!TIP]
   >
   >Atualize o tipo de recurso, pois ele agora é DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Teste sua configuração.
