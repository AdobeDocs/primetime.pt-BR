---
description: Para receber notificações sobre tags no manifesto, ouça AdobePSDK.TimedMetadataEvent.
seo-description: Para receber notificações sobre tags no manifesto, ouça AdobePSDK.TimedMetadataEvent.
seo-title: Adicionar ouvintes para notificações de metadados cronometrados
title: Adicionar ouvintes para notificações de metadados cronometrados
uuid: c82c5549-0ab6-4343-a766-5176e784d4cb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Adicionar ouvintes para notificações de metadados cronometrados{#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, ouça AdobePSDK.TimedMetadataEvent.

Quando um novo `TimedMetadata` objeto é criado, o MediaPlayer despacha `AdobePSDK.TimedMetadataEvent`.

1. Implemente os ouvintes apropriados.

   ```js
   function onTimedMetadataEvent(event) { 
       var timedMetadata = event.timedMetadata; 
       // process the timed metadata collection 
       } 
   ```

1. Registre os ouvintes de evento.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.TIMED_METADATA_AVAILABLE, onTimedMetadataEvent);
   ```

Os metadados ID3 são enviados pelo mesmo `Events.TimedMetadataEvent`. Você pode usar a `timedMetadata.type` propriedade para distinguir entre TAG e ID3.

