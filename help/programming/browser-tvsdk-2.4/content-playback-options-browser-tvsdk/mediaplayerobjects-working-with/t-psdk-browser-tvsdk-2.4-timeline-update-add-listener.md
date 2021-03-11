---
description: Para receber notificações sobre atualizações de linha do tempo, registre os ouvintes de eventos apropriados.
title: Adicionar ouvintes para TimelineUpdatedEvent
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---


# Adicionar ouvintes para TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Para receber notificações sobre atualizações de linha do tempo, registre os ouvintes de eventos apropriados.

Cada vez que a linha do tempo é atualizada, o `MediaPlayer` despacha `AdobePSDK.TimelineEvent` com o tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
1. Implemente os ouvintes apropriados.

   ```js
   function onTimelineUpdatedEvent(event) { 
       var timelineMarkers = event.timeline.timelineMarkers; 
       //add code to remove old timeline markers from scrub-bar. 
       var range = player.playbackRange; 
       //iterate through the list of timelineMarkers 
       for(var i = 0; i < timelineMarkers.length; i++) 
       { 
           var markerLocalTime = timelineMarkers[i].localRange.begin; 
           var markerVirtualTime = timelineMarkers[i].virtualRange.begin; 
           var duration = timelineMarkers[i].duration; 
        // add code to draw a particular marker on scrub-bar 
       }      
   }
   ```

1. Registre os ouvintes do evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

