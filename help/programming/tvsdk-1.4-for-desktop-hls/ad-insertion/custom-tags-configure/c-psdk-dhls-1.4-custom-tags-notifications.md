---
description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia. A propriedade MediaPlayerItem.hasTimedMetadata indica se uma tag personalizada assinada está presente na mídia atual.
seo-description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia. A propriedade MediaPlayerItem.hasTimedMetadata indica se uma tag personalizada assinada está presente na mídia atual.
seo-title: Notificações para tags manifest
title: Notificações para tags manifest
uuid: 87bee41b-b44e-4d12-afd2-7a63023f992c
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# Notificações para marcas de manifesto{#notifications-for-manifest-tags}

A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia. A propriedade MediaPlayerItem.hasTimedMetadata indica se uma tag personalizada assinada está presente na mídia atual.

Você pode monitorar os metadados cronometrados ouvindo os seguintes eventos, que notificam sua aplicação da atividade relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: A lista inicial de  `TimedMetadata` objetos está disponível depois que o objeto  `MediaPlayerItem` é criado. Este evento notifica seu aplicativo quando isso acontece.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para fluxos ao vivo/lineares nos quais o manifesto/lista de reprodução é atualizado periodicamente, outras tags personalizadas podem aparecer na lista de reprodução/manifesto atualizado, portanto, objetos TimedMetadata adicionais podem ser adicionados à  `MediaPlayerItem.timedMetadata` propriedade. Este evento notifica seu aplicativo quando isso acontece.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Toda vez que um novo  `TimedMetadata` objeto é criado, esse evento é despachado pelo  `MediaPlayer`. Este evento não é despachado para o objeto `TimedMetadata` criado durante a fase de inicialização.

