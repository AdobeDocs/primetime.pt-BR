---
description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.
seo-description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.
seo-title: Notificações para tags manifest
title: Notificações para tags manifest
uuid: 50727455-b37b-4e39-8efb-a97de3164074
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Notificações para tags manifest{#notifications-for-manifest-tags}

A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

A `MediaPlayerItem.hasTimedMetadata` propriedade indica se uma tag personalizada assinada existe na mídia atual. Você pode monitorar metadados cronometrados ouvindo o `Events.TimedMetadataEvent`, que a instância do MediaPlayer despacha sempre que um novo `TimedMetadata` objeto é criado.
