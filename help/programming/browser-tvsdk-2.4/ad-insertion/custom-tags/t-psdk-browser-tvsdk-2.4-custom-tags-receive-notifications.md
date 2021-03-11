---
description: Para receber notificações sobre tags no manifesto, ouça AdobePSDK.TimedMetadataEvent.
title: Adicionar ouvintes para notificações de metadados cronometrados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---


# Adicionar ouvintes para notificações de metadados cronometrados{#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, ouça AdobePSDK.TimedMetadataEvent.

Quando um novo objeto `TimedMetadata` é criado, o MediaPlayer envia `AdobePSDK.TimedMetadataEvent`.

1. Implemente os ouvintes apropriados.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registre os ouvintes do evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

Os metadados ID3 são despachados por meio do mesmo `Events.TimedMetadataEvent`. Você pode usar a propriedade `timedMetadata.type` para distinguir entre TAG e ID3.

