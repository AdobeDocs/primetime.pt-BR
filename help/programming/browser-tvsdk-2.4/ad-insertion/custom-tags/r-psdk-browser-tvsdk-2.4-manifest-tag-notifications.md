---
description: A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados nas tags de lista de reprodução/manifesto ou nas tags ID3 no fluxo de mídia.
title: Notificações para tags de manifesto
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Notificações para tags de manifesto{#notifications-for-manifest-tags}

A propriedade MediaPlayerItem.timedMetadata fornece acesso a todos os objetos TimedMetadata criados nas tags de lista de reprodução/manifesto ou nas tags ID3 no fluxo de mídia.

<!--<a id="section_9A22F6F1EA1F4F0C9E0C7687D12AA4AA"></a>-->

A variável `MediaPlayerItem.hasTimedMetadata` indica se uma tag personalizada assinada existe na mídia atual. Você pode monitorar os metadados cronometrados ouvindo a `Events.TimedMetadataEvent`, que a ocorrência de MediaPlayer despacha cada vez que um novo `TimedMetadata` objeto é criado.
