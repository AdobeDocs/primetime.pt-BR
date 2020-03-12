---
description: Para receber notificações sobre atualizações de linha do tempo, registre os ouvintes de evento apropriados.
seo-description: Para receber notificações sobre atualizações de linha do tempo, registre os ouvintes de evento apropriados.
seo-title: Adicionar ouvintes para Linha do tempoAtualizadoEvent
title: Adicionar ouvintes para Linha do tempoAtualizadoEvent
uuid: 7d742e15-5a55-4155-93a7-7b79f21c1472
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Adicionar ouvintes para Linha do tempoAtualizadoEvent{#add-listeners-for-timelineupdatedevent}

Para receber notificações sobre atualizações de linha do tempo, registre os ouvintes de evento apropriados.

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

1. Registre os ouvintes de evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMELINE_UPDATED,  
       onTimelineUpdatedEvent);
   ```

