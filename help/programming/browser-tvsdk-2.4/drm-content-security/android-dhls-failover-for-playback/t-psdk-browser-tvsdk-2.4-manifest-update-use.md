---
description: Você pode ativar esse recurso e verificar eventos relacionados.
title: Usar atualização de manifesto principal em tempo real
exl-id: 02cb3116-cc30-4139-841b-8d6297214b8b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '56'
ht-degree: 0%

---

# Usar atualização de manifesto principal em tempo real{#use-live-master-manifest-update}

Você pode ativar esse recurso e verificar eventos relacionados.

1. Para ativar as atualizações de manifesto principal ao vivo, defina a frequência de atualização (em minutos) definindo o `NetworkConfiguration.masterUpdateInterval` propriedade.
1. Como opção, rastreie as atualizações bem-sucedidas do manifesto ouvindo o `MediaPlayerItemEvent.MASTER_UPDATED` evento.
