---
description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados nas tags de lista de reprodução/manifesto ou nas tags ID3 no fluxo de mídia. A propriedade MediaPlayerItem.hasTimedMetadata indica se uma tag personalizada inscrita está presente na mídia atual.
title: Notificações para tags de manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '188'
ht-degree: 0%

---

# Notificações para tags de manifesto{#notifications-for-manifest-tags}

A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados nas tags de lista de reprodução/manifesto ou nas tags ID3 no fluxo de mídia. A propriedade MediaPlayerItem.hasTimedMetadata indica se uma tag personalizada inscrita está presente na mídia atual.

Você pode monitorar metadados cronometrados ouvindo os seguintes eventos, que notificam seu aplicativo sobre atividades relacionadas:

* `MediaPlayerItemEvent.ITEM_CREATED`: a lista inicial de `TimedMetadata` objetos estiver disponível após a variável `MediaPlayerItem` é criado. Esse evento notifica seu aplicativo quando isso ocorre.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para fluxos ao vivo/lineares nos quais o manifesto/lista de reprodução é atualizado periodicamente, tags personalizadas adicionais podem aparecer na lista de reprodução/manifesto atualizada, portanto, objetos TimedMetadata adicionais podem ser adicionados à `MediaPlayerItem.timedMetadata` propriedade. Esse evento notifica seu aplicativo quando isso ocorre.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: toda vez que um novo `TimedMetadata` for criado, esse evento será despachado pelo `MediaPlayer`. Este evento não é despachado para o `TimedMetadata` objeto criado durante a fase de inicialização.
