---
description: Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de evento apropriado(s).
title: Adicionar ouvintes para notificações de metadados cronometrados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---


# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de evento apropriado(s).

Você pode monitorar metadados cronometrados escutando os seguintes eventos, que notificam o aplicativo da atividade relacionada:

* `onTimedMetadata`: Cada vez que uma tag assinada exclusiva é identificada durante a análise do conteúdo, o TVSDK prepara um novo  `TimedMetadata` objeto e despacha esse evento.

   O objeto contém o nome da tag da qual você se inscreveu, o horário local na reprodução em que essa tag será exibida e outros dados.

   Escute os eventos.

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

Os metadados ID3 usam o mesmo ouvinte onTimedMetadata para indicar a presença de uma tag ID3. No entanto, isso não deve causar confusão, pois é possível usar uma propriedade `TimedMetadata` do objeto `type` para diferenciar entre TAG e ID3. Para obter mais informações sobre as tags ID3, consulte [ID3 tags](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
