---
description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis. O player pode implementar ações em resposta a esses eventos.
seo-description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis. O player pode implementar ações em resposta a esses eventos.
seo-title: Eventos DRM
title: Eventos DRM
uuid: 729fe524-1047-4188-b4e6-96bfc5af4ae0
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Eventos DRM{#drm-events}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis. O player pode implementar ações em resposta a esses eventos.

Para ser notificado sobre todos os eventos relacionados ao DRM, ouça o seguinte:

```
DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE
```

O exemplo a seguir mostra uma progressão típica:

```
mediaPlayer.addEventListener(DRMMetadataInfoEvent.DRM_METADATA_INFO_AVAILABLE,  
                             onDRMMetadataInfoAvailable);   
private function onDRMMetadataInfoAvailable(event:DRMMetadataInfoEvent){ 
    var drmMetadataInfo:DRMMetadataInfo = event.drmMetadataInfo; 
    ... 
} 
```

