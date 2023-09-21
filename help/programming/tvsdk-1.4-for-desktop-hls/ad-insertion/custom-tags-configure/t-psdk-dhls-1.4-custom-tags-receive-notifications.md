---
description: Para receber notificações sobre tags no manifesto, registre os ouvintes de eventos apropriados.
title: Adicionar ouvintes para notificações de metadados cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Adicionar ouvintes para notificações de metadados cronometrados{#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, registre os ouvintes de eventos apropriados.

Você pode monitorar metadados cronometrados ouvindo os seguintes eventos, que notificam seu aplicativo sobre atividades relacionadas:

* `MediaPlayerItemEvent.ITEM_CREATED`: a lista inicial de `TimedMetadata` objetos estiver disponível após a variável `MediaPlayerItem` é criado.

  Esse evento notifica seu aplicativo quando isso ocorre.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para fluxos ao vivo/lineares nos quais o manifesto/lista de reprodução é atualizado periodicamente, tags personalizadas adicionais podem aparecer na lista de reprodução/manifesto atualizada, portanto, tags adicionais `TimedMetadata` objetos podem ser adicionados à `MediaPlayerItem.timedMetadata` propriedade.

  Esse evento notifica seu aplicativo quando isso ocorre.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: cada vez que um novo `TimedMetadata` for criado, esse evento será despachado pelo MediaPlayer.

  Este evento não é despachado para o `TimedMetadata` objeto criado durante a fase de inicialização.

1. Implemente os ouvintes apropriados.

   ```
   private function onItemCreated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onItemUpdated(event:MediaPlayerItemEvent):void { 
       var timedMetadataCollection:Vector.<TimedMetadata> = event.item.timedMetadata; 
       // process the timed metadata collection 
   } 
   
   private function onTimedMetadataAvailable(event:TimedMetadataEvent):void { 
       var timedMetadata:TimedMetadata = event.timedMetadata; 
       // process timed metadata 
   }
   ```

1. Registre os ouvintes de eventos.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

Os metadados de ID3 são despachados pelo mesmo `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. No entanto, isso não deve causar confusão, pois é possível usar as propriedades de um objeto TimedMetadata `type` para diferenciar entre TAG e ID3. Para obter mais informações sobre tags ID3, consulte [Tags ID3](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).
