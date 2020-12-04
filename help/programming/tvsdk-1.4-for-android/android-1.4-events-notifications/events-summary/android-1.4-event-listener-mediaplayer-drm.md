---
description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis.
seo-description: O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis.
seo-title: Eventos DRM
title: Eventos DRM
uuid: c4d96e06-2268-4e38-9d05-68ccbe912484
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '104'
ht-degree: 0%

---


# Eventos DRM{#drm-events}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis.

Para ser notificado sobre todos os eventos relacionados ao DRM, registre uma implementação de `MediaPlayer.DRMEventListener` que inclua o seguinte retorno de chamada.

| Evento | Significado |
|---|---|
| [onDRMMetadata](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayer.DRMEventListener.html#onDRMMetadata(DRMMetadataInfo)) `(DRMMetadataInfo drmMetadataInfo)` | Os novos metadados DRM estão disponíveis. |

