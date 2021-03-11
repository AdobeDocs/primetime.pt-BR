---
description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas a DRM, como quando novos metadados de DRM são disponibilizados.
title: Eventos DRM
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---


# Eventos DRM{#drm-events}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas a DRM, como quando novos metadados de DRM são disponibilizados.

Para ser notificado sobre todos os eventos relacionados ao DRM, registre uma implementação de `MediaPlayer.DRMEventListener` que inclui o retorno de chamada a seguir.

| Evento | Significado |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Novos metadados de DRM estão disponíveis. |

