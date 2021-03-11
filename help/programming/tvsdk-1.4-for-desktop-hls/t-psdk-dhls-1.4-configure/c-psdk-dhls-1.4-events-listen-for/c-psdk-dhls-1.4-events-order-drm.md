---
description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas a DRM, como quando novos metadados de DRM são disponibilizados. O reprodutor pode implementar ações em resposta a esses eventos.
title: Eventos DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Eventos DRM{#drm-events}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas a DRM, como quando novos metadados de DRM são disponibilizados. O reprodutor pode implementar ações em resposta a esses eventos.

Para ser notificado sobre todos os eventos relacionados a DRM, analise o seguinte:

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

