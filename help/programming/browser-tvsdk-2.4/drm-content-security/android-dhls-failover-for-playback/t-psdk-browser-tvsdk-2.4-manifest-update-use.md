---
description: Você pode ativar esse recurso e verificar eventos relacionados.
seo-description: Você pode ativar esse recurso e verificar eventos relacionados.
seo-title: Usar atualização live principal-manifest
title: Usar atualização live principal-manifest
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Usar a atualização live principal-manifest{#use-live-master-manifest-update}

Você pode ativar esse recurso e verificar eventos relacionados.

1. Para ativar atualizações principais e manifestas ao vivo, defina a frequência de atualização (em minutos) definindo a propriedade `NetworkConfiguration.masterUpdateInterval`.
1. Como opção, rastreie atualizações de manifesto bem-sucedidas ao acompanhar o evento `MediaPlayerItemEvent.MASTER_UPDATED`.
