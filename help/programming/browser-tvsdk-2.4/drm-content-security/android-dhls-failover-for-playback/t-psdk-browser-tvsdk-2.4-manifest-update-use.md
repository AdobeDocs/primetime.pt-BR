---
description: Você pode ativar esse recurso e verificar eventos relacionados.
seo-description: Você pode ativar esse recurso e verificar eventos relacionados.
seo-title: Usar atualização do manifesto mestre ativo
title: Usar atualização do manifesto mestre ativo
uuid: 4ec665ab-b7ce-4a45-a251-13a07eb4d789
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Usar atualização do manifesto mestre ativo{#use-live-master-manifest-update}

Você pode ativar esse recurso e verificar eventos relacionados.

1. Para ativar as atualizações do manifesto mestre ativo, defina a frequência de atualização (em minutos) definindo a `NetworkConfiguration.masterUpdateInterval` propriedade.
1. Como opção, rastreie atualizações de manifesto bem-sucedidas ao acompanhar o `MediaPlayerItemEvent.MASTER_UPDATED` evento.
