---
description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados de DRM são disponibilizados. Seu reprodutor pode implementar ações em resposta a esses eventos.
title: Eventos DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Eventos DRM{#drm-events}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados de DRM são disponibilizados. Seu reprodutor pode implementar ações em resposta a esses eventos.

Para ser notificado sobre todos os eventos relacionados ao DRM, acompanhe o seguinte:

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
