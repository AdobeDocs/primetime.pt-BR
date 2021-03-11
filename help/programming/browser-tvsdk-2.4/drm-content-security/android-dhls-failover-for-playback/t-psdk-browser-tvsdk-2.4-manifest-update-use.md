---
description: Você pode ativar esse recurso e verificar eventos relacionados.
title: Usar atualização de manifesto principal ao vivo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---


# Usar atualização de manifesto principal ao vivo{#use-live-master-manifest-update}

Você pode ativar esse recurso e verificar eventos relacionados.

1. Para ativar atualizações de manifesto principal ao vivo, defina a frequência de atualização (em minutos) definindo a propriedade `NetworkConfiguration.masterUpdateInterval`.
1. Como opção, rastreie atualizações de manifesto bem-sucedidas ao acompanhar o evento `MediaPlayerItemEvent.MASTER_UPDATED` .
