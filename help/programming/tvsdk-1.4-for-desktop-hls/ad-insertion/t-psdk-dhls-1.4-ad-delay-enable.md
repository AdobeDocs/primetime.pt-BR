---
description: Você pode especificar se deseja permitir a reprodução antes que todos os anúncios sejam carregados e colocados na linha do tempo. Iniciar a reprodução dessa maneira fornece ao visualizador acesso mais rápido ao conteúdo principal. Esse recurso é aplicável somente para DVR ao vivo e não funciona, digamos, em ativos de VOD.
title: Habilitar carregamento lento de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---

# Habilitar carregamento lento de anúncios{#enable-lazy-ad-loading}

Você pode especificar se deseja permitir a reprodução antes que todos os anúncios sejam carregados e colocados na linha do tempo. Iniciar a reprodução dessa maneira fornece ao visualizador acesso mais rápido ao conteúdo principal. Esse recurso é aplicável somente para DVR ao vivo e não funciona, digamos, em ativos de VOD.

1. Usar a propriedade booleana `delayAdLoading` in `AdvertisingMetadata`.

   * Quando for falso, o TVSDK aguardará até que todos os anúncios sejam resolvidos e colocados antes da transição para o status PREPARADO. É falso por padrão.
   * Quando verdadeiro, o TVSDK resolve somente os anúncios iniciais e faz a transição para o status PREPARADO. Os anúncios restantes são resolvidos e colocados durante a reprodução.

1. Para ativar também o carregamento atrasado de anúncios com o Adobe Primetime ad decisioning, defina como `true` ao criar `AuditudeSettings`.

   A variável `AuditudeSettings` a classe herda essa propriedade de `AdvertisingMetadata`, mas não herda o valor atual.

   ```
   var auditudeSettings:AuditudeSettings = new AuditudeSettings(); 
   auditudeSettings.mediaId = ... 
   auditudeSettings.zoneId = ... 
   auditudeSettings.delayAdLoading = true;
   ```

1. Para refletir com precisão os anúncios como dicas em uma barra de limpeza, acompanhe o `TimelineEvent`. `TIMELINE_UPDATED` e redesenhe a barra de limpeza toda vez que receber esse evento.

   Quando os fluxos de VoD usam o carregamento atrasado de anúncios, nem todos os anúncios são colocados na linha do tempo quando o reprodutor entra no status PREPARADO, portanto, você deve redesenhar explicitamente a barra de depuração.

   O TVSDK otimiza o despacho desse evento para minimizar o número de vezes que você deve redesenhar a barra de depuração; portanto, o número de eventos na linha do tempo não está relacionado ao número de ad breaks a serem colocados na linha do tempo. Por exemplo, se você tiver cinco ad breaks, talvez não receba exatamente cinco eventos.

   ```
   mediaPlayer.addEventListener(TimelineEvent.TIMELINE_UPDATED, onTimelineUpdated); 
   // ... 
   function onTimelineUpdated(event:TimelineEvent):void { 
       // get markers 
       var markers:Vector.<TimelineMarker> = event.timeline.timelineMarkers; 
       drawMarkers(markers); 
   } 
   ```
