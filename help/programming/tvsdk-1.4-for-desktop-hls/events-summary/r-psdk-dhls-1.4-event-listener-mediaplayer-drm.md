---
description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados de DRM são disponibilizados.
title: Eventos DRM
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 0%

---

# Eventos DRM{#drm-events}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados de DRM são disponibilizados.

Para ser notificado sobre todos os eventos relacionados ao DRM, acompanhe `DRMMetadataInfoEvent` para eventos DRM com a variável `MediaPlayer` objeto.

| Evento | Significado |
|---|---|
| DRMMetadataInfoEvent.[DRM_METADATA_INFO_AVAILABLE](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/events/DRMMetadataInfoEvent.html#DRM_METADATA_INFO_AVAILABLE) | Novos metadados de DRM estão disponíveis. |
