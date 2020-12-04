---
description: Você pode concluir workflows específicos de Digital Rights Management (DRM).
seo-description: Você pode concluir workflows específicos de Digital Rights Management (DRM).
seo-title: Digital Rights Management
title: Digital Rights Management
uuid: 011605c7-50c4-4ad5-9961-8cd92d0e6fd8
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 0%

---


# Digital Rights Management {#digital-rights-management}

Você pode concluir workflows específicos de Digital Rights Management (DRM).

Você pode ouvir o evento `AdobePSDK.DRMMetadataInfoEvent` para lidar com workflows DRM:

```js
... 
player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvailable);
...
```

## Adicionar Digital Rights Management {#add-digital-rights-management}

1. Adicione `DRMMetadataInfoAvailableEvent` para obter o `DRMMetadata`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.DRM_METADATA_INFO_AVAILABLE, onDRMMetadataInfoAvaialble);
   ```

1. Implemente a seção `onDRMMetadataInfoAvailable` acima da linha na etapa 1.

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

1. Crie os dados de proteção para Widevine e PlayReady copiando a seguinte amostra:

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
   >Certifique-se de atualizar o tipo de recurso, pois agora é DASH.

   ```js
   var resourceUrl = "https://ptdemos.com/videos/dashdrm/stream.mpd"; 
   var resourceType = AdobePSDK.MediaResourceType.DASH;
   ```

1. Teste sua configuração.