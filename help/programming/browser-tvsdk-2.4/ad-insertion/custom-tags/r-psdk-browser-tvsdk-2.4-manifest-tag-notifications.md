---
description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.
seo-description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.
seo-title: Notificações para tags manifest
title: Notificações para tags manifest
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Notificações para marcas de manifesto{#notifications-for-manifest-tags}

A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

A propriedade `MediaPlayerItem.hasTimedMetadata` indica se existe uma tag personalizada subscrita na mídia atual. Você pode monitorar os metadados programados ouvindo `Events.TimedMetadataEvent`, que a instância do MediaPlayer envia sempre que um novo objeto `TimedMetadata` é criado.
