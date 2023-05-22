---
description: Para receber notificações sobre atualizações de linha do tempo, registre os ouvintes de eventos apropriados.
title: Adicionar ouvintes para TimelineUpdatedEvent
exl-id: 7b55beb5-fd84-4144-8d02-bbd998f99e3a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '47'
ht-degree: 0%

---

# Adicionar ouvintes para TimelineUpdatedEvent{#add-listeners-for-timelineupdatedevent}

Para receber notificações sobre atualizações de linha do tempo, registre os ouvintes de eventos apropriados.

Cada vez que a linha do tempo é atualizada, a variável `MediaPlayer` expedições `AdobePSDK.TimelineEvent` com tipo `AdobePSDK.PSDKEventType.TIMELINE_UPDATED`.
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

1. Registre os ouvintes de eventos.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```
