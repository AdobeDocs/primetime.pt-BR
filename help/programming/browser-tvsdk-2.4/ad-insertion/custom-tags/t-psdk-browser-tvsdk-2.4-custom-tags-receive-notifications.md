---
description: Para receber notificações sobre tags no manifesto, acompanhe AdobePSDK.TimedMetadataEvent.
title: Adicionar ouvintes para notificações de metadados cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '67'
ht-degree: 0%

---

# Adicionar ouvintes para notificações de metadados cronometrados{#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, acompanhe AdobePSDK.TimedMetadataEvent.

Quando um novo `TimedMetadata` for criado, o MediaPlayer enviará `AdobePSDK.TimedMetadataEvent`.

1. Implemente os ouvintes apropriados.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registre os ouvintes de eventos.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

Os metadados de ID3 são despachados pelo mesmo `Events.TimedMetadataEvent`. Você pode usar o `timedMetadata.type` para distinguir entre TAG e ID3.
