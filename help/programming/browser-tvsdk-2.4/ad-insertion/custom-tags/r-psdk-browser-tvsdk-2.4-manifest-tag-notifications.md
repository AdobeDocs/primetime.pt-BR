---
description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.
title: Notificações para tags de manifesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Notificações para tags de manifesto{#notifications-for-manifest-tags}

A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

A propriedade `MediaPlayerItem.hasTimedMetadata` indica se uma tag personalizada subscrita existe na mídia atual. Você pode monitorar metadados cronometrados escutando o `Events.TimedMetadataEvent`, que a instância MediaPlayer envia sempre que um novo objeto `TimedMetadata` é criado.
