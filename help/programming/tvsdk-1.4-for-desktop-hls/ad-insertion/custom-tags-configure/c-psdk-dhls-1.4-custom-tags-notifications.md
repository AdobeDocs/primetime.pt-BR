---
description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia. A propriedade MediaPlayerItem.hasTimedMetadata indica se uma tag personalizada subscrita está presente na mídia atual.
title: Notificações para tags de manifesto
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---


# Notificações para tags de manifesto{#notifications-for-manifest-tags}

A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados a partir de tags playlist/manifest ou de tags ID3 no fluxo de mídia. A propriedade MediaPlayerItem.hasTimedMetadata indica se uma tag personalizada subscrita está presente na mídia atual.

Você pode monitorar metadados cronometrados escutando os seguintes eventos, que notificam o aplicativo da atividade relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: A lista inicial de  `TimedMetadata` objetos está disponível depois que o  `MediaPlayerItem` é criado. Esse evento notifica seu aplicativo quando isso acontece.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para fluxos ao vivo/lineares onde o manifesto/lista de reprodução é atualizado periodicamente, tags personalizadas adicionais podem aparecer na lista de reprodução/manifesto atualizado, portanto, objetos TimedMetadata adicionais podem ser adicionados à  `MediaPlayerItem.timedMetadata` propriedade. Esse evento notifica seu aplicativo quando isso acontece.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Toda vez que um novo  `TimedMetadata` objeto é criado, esse evento é despachado pelo  `MediaPlayer`. Esse evento não é despachado para o objeto `TimedMetadata` criado durante a fase de inicialização.

