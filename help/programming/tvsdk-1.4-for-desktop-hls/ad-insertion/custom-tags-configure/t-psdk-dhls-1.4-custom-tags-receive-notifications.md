---
description: Para receber notificações sobre tags no manifesto, registre os ouvintes de evento apropriados.
seo-description: Para receber notificações sobre tags no manifesto, registre os ouvintes de evento apropriados.
seo-title: Adicionar ouvintes para notificações de metadados cronometrados
title: Adicionar ouvintes para notificações de metadados cronometrados
uuid: 419f4204-e3c3-4608-beb4-4cd259c8474d
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Adicionar ouvintes para notificações de metadados cronometrados{#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, registre os ouvintes de evento apropriados.

Você pode monitorar os metadados cronometrados ouvindo os seguintes eventos, que notificam sua aplicação da atividade relacionada:

* `MediaPlayerItemEvent.ITEM_CREATED`: A lista inicial de  `TimedMetadata` objetos está disponível depois que o objeto  `MediaPlayerItem` é criado.

   Este evento notifica seu aplicativo quando isso acontece.

* `MediaPlayerItemEvent.ITEM_UPDATED`: Para fluxos ao vivo/lineares nos quais o manifesto/lista de reprodução é atualizado periodicamente, outras tags personalizadas podem aparecer na lista de reprodução/manifesto atualizado, portanto,  `TimedMetadata` objetos adicionais podem ser adicionados à  `MediaPlayerItem.timedMetadata` propriedade.

   Este evento notifica seu aplicativo quando isso acontece.

* `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`: Cada vez que um novo  `TimedMetadata` objeto é criado, esse evento é despachado pelo MediaPlayer.

   Este evento não é despachado para o objeto `TimedMetadata` criado durante a fase de inicialização.

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

Os metadados ID3 são enviados pelo mesmo `TimedMetadataEvent.TIMED_METADATA_AVAILABLE`. No entanto, isso não deve causar confusão, pois você pode usar uma propriedade `type` do objeto TimedMetadata para diferenciar entre TAG e ID3. Para obter mais informações sobre tags ID3, consulte [tags ID3](../../../tvsdk-1.4-for-desktop-hls/r-psdk-dhls-1.4-notification-system/notification-system/t-psdk-dhls-1.4-id3-metadata-retrieve.md).