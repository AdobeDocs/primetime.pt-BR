---
description: É possível especificar se a reprodução deve ser permitida antes de todos os anúncios serem carregados e colocados na linha do tempo. Iniciar a reprodução dessa forma dá ao visualizador acesso mais rápido ao conteúdo principal. Este recurso é aplicável somente para DVR ao vivo e não funciona, digamos, em ativos VOD.
seo-description: É possível especificar se a reprodução deve ser permitida antes de todos os anúncios serem carregados e colocados na linha do tempo. Iniciar a reprodução dessa forma dá ao visualizador acesso mais rápido ao conteúdo principal. Este recurso é aplicável somente para DVR ao vivo e não funciona, digamos, em ativos VOD.
seo-title: Ativar carregamento de anúncio lento
title: Ativar carregamento de anúncio lento
uuid: ac7c8801-7fa2-4f17-b79c-c603b3236948
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Ativar carregamento de anúncio lento{#enable-lazy-ad-loading}

É possível especificar se a reprodução deve ser permitida antes de todos os anúncios serem carregados e colocados na linha do tempo. Iniciar a reprodução dessa forma dá ao visualizador acesso mais rápido ao conteúdo principal. Este recurso é aplicável somente para DVR ao vivo e não funciona, digamos, em ativos VOD.

1. Use a propriedade Booliana `delayAdLoading` em `AdvertisingMetadata`.

   * Quando falso, o TVSDK aguarda até que todos os anúncios sejam resolvidos e colocados antes da transição para o status PREPARADO. Por padrão, é falso.
   * Quando verdadeiro, o TVSDK resolve somente os anúncios e transições iniciais para o status PREPARADO. Os anúncios restantes são resolvidos e colocados durante a reprodução.

1. Para ativar também o carregamento atrasado do anúncio com a decisão do anúncio do Adobe Primetime, defina para `true` quando você criar `AuditudeSettings`.

   A `AuditudeSettings` classe herda essa propriedade de `AdvertisingMetadata`, mas não herda o valor atual.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Para refletir com precisão as publicidades como dicas em uma barra de depuração, ouça o `TimelineEvent`. `TIMELINE_UPDATED` e redesenhe a barra de depuração sempre que receber esse evento.

   Quando os fluxos VoD usam o carregamento atrasado do anúncio, nem todos os anúncios são colocados na linha do tempo quando o player entra no status PREPARADO, portanto, você deve redesenhar explicitamente a barra de depuração.

   O TVSDK otimiza o despacho desse evento para minimizar o número de vezes que você deve redesenhar a barra de depuração; portanto, o número de eventos de linha do tempo não está relacionado ao número de quebras de anúncios a serem colocadas na linha do tempo. Por exemplo, se você tiver cinco pausas de anúncio, talvez você não receba exatamente cinco eventos.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

