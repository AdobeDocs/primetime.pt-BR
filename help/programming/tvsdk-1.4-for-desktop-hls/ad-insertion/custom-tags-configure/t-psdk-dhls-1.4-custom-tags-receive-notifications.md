---
description: Para receber notificações sobre tags no manifesto, registre os ouvintes de eventos apropriados.
title: Adicionar ouvintes para notificações de metadados cronometrados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Adicionar ouvintes para notificações de metadados cronometrados{#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, registre os ouvintes de eventos apropriados.

Você pode monitorar metadados cronometrados escutando os seguintes eventos, que notificam o aplicativo da atividade relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: A lista inicial de  `TimedMetadata` objetos está disponível depois que o  `MediaPlayerItem` é criado.

   Esse evento notifica seu aplicativo quando isso acontece.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para fluxos ao vivo/lineares onde o manifesto/lista de reprodução é atualizado periodicamente, tags personalizadas adicionais podem aparecer na lista de reprodução/manifesto atualizado, portanto,  `TimedMetadata` objetos adicionais podem ser adicionados à  `MediaPlayerItem.timedMetadata` propriedade.

   Esse evento notifica seu aplicativo quando isso acontece.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Cada vez que um novo  `TimedMetadata` objeto é criado, esse evento é enviado pelo MediaPlayer.

   Esse evento não é despachado para o objeto `TimedMetadata` criado durante a fase de inicialização.

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

1. Registre os ouvintes do evento.

   ```
   player.addEventListener(MediaPlayerItemEvent.ITEM_CREATED, onItemCreated); 
   player.addEventListener(MediaPlayerItemEvent.ITEM_UPDATED, onItemUpdated); 
   player.addEventListener(TimedMetadataEvent.TIMED_METADATA_AVAILABLE,  
                           onTimedMetadataAvailable);
   ```

Os metadados ID3 são despachados por meio do mesmo `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. No entanto, isso não deve causar confusão, pois é possível usar a propriedade `type` de um objeto TimedMetadata para diferenciar entre TAG e ID3. Para obter mais informações sobre as tags ID3, consulte [ID3 tags](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).