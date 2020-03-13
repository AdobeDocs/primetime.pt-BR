---
description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis.
seo-description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis.
seo-title: Eventos DRM
title: Eventos DRM
uuid: f1da5b31-3fad-4bb4-8aa3-3925d5f0e123
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# Eventos DRM{#drm-events}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis.

Para ser notificado sobre todos os eventos relacionados ao DRM, monitore os eventos `DRMMetadataInfoEvent` do DRM com o `MediaPlayer` objeto.

| Evento | Significado |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Os novos metadados DRM estão disponíveis. |