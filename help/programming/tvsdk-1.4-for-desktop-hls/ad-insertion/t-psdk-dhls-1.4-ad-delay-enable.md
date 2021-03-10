---
description: Você pode especificar se a reprodução deve ser permitida antes que todos os anúncios sejam carregados e colocados na linha do tempo. Iniciar a reprodução dessa forma fornece ao visualizador acesso mais rápido ao conteúdo principal. Esse recurso é aplicável somente para DVR ao vivo e não funciona em, digamos, ativos VOD.
title: Habilitar carregamento lento de anúncio
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# Habilitar carregamento lento de anúncio{#enable-lazy-ad-loading}

Você pode especificar se a reprodução deve ser permitida antes que todos os anúncios sejam carregados e colocados na linha do tempo. Iniciar a reprodução dessa forma fornece ao visualizador acesso mais rápido ao conteúdo principal. Esse recurso é aplicável somente para DVR ao vivo e não funciona em, digamos, ativos VOD.

1. Use a propriedade booleana `delayAdLoading` em `AdvertisingMetadata`.

   * Quando falso, o TVSDK aguarda até que todos os anúncios sejam resolvidos e colocados antes da transição para o status PREPARADO. É falso por padrão.
   * Quando verdadeiro, o TVSDK resolve apenas os anúncios iniciais e faz a transição para o status PREPARADO. Os anúncios restantes são resolvidos e colocados durante a reprodução.

1. Para também ativar o carregamento atrasado do anúncio com a decisão do anúncio do Adobe Primetime, defina como `true` ao criar `AuditudeSettings`.

   A classe `AuditudeSettings` herda essa propriedade de `AdvertisingMetadata`, mas não herda o valor atual.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Para refletir com precisão os anúncios como dicas em uma barra de depuração, escute o `TimelineEvent`. `TIMELINE_UPDATED` e refaça a barra de depuração sempre que receber esse evento.

   Quando os fluxos de VoD usam o carregamento atrasado do anúncio, nem todos os anúncios são colocados na linha do tempo quando o reprodutor entra no status PREPARED , portanto, você deve redesenhar explicitamente a barra de depuração.

   O TVSDK otimiza o despacho desse evento para minimizar o número de vezes que você deve redesenhar a barra de depuração; portanto, o número de eventos de linha do tempo não está relacionado ao número de ad breaks a serem colocados na linha do tempo. Por exemplo, se você tiver cinco ad breaks, talvez você não receba exatamente cinco eventos.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```

