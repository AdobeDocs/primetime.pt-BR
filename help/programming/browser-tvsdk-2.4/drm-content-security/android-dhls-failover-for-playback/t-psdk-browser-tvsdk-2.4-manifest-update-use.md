---
description: Você pode ativar esse recurso e verificar eventos relacionados.
title: Usar atualização ao vivo do manifesto principal
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Usar atualização ao vivo do manifesto principal{#use-live-master-manifest-update}

Você pode ativar esse recurso e verificar eventos relacionados.

1. Para ativar as atualizações ao vivo do manifesto principal, defina a frequência de atualização (em minutos) definindo o `NetworkConfiguration.masterUpdateInterval` propriedade.
1. Como opção, rastreie as atualizações bem-sucedidas do manifesto ouvindo o `MediaPlayerItemEvent.MASTER_UPDATED` evento.
