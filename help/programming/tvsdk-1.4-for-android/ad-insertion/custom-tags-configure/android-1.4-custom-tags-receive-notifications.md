---
description: Para receber notificações sobre tags no manifesto, implemente os ouvintes de evento apropriados.
seo-description: Para receber notificações sobre tags no manifesto, implemente os ouvintes de evento apropriados.
seo-title: Adicionar ouvintes para notificações de metadados cronometrados
title: Adicionar ouvintes para notificações de metadados cronometrados
uuid: cd7a5936-d63a-4711-ac16-2d79bac099a3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 0%

---


# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, implemente os ouvintes de evento apropriados.

Você pode monitorar os metadados cronometrados ouvindo os seguintes eventos, que notificam sua aplicação da atividade relacionada:

* `onTimedMetadata`: Cada vez que uma tag assinada exclusiva é identificada durante a análise do conteúdo, o TVSDK prepara um novo  `TimedMetadata` objeto e despacha esse evento.

   O objeto contém o nome da tag na qual você se inscreveu, a hora local na reprodução em que essa tag será exibida e outros dados.

   Ouça eventos.

   ```java
   private final TimedMetadataEventListener timedMetadataEventListener =  
     new TimedMetadataEventListener() { 
       @Override 
       public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { 
           TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata(); 
   
           TimedMetadata.Type type = timedMetadata.getType(); 
           if (type.equals(TimedMetadata.Type.ID3)){ 
               Metadata metadata = timedMetadata.getMetadata(); 
               Set<String> keys = metadata.keySet(); 
               for (String key : keys) { 
                   String value = metadata.getValue(key); 
               } 
           } else if (_mediaPlayer.getPlaybackRange() !=  
                      null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
               displayRanges(); 
           } 
       } 
   }; 
   ```

Os metadados ID3 usam o mesmo ouvinte onTimedMetadata para indicar a presença de uma tag ID3. No entanto, isso não deve causar confusão, pois você pode usar uma propriedade `TimedMetadata` do objeto `type` para diferenciar entre TAG e ID3. Para obter mais informações sobre tags ID3, consulte [tags ID3](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
