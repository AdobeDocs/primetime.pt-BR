---
description: Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de eventos apropriado(s).
title: Adicionar ouvintes para notificações de metadados cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '153'
ht-degree: 0%

---

# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de eventos apropriado(s).

Você pode monitorar metadados cronometrados ouvindo os seguintes eventos, que notificam seu aplicativo sobre atividades relacionadas:

* `onTimedMetadata`: Cada vez que uma tag única assinada é identificada durante a análise do conteúdo, o TVSDK prepara uma nova `TimedMetadata` e despacha esse evento.

  O objeto contém o nome da tag que você assinou, o horário local na reprodução em que essa tag aparecerá e outros dados.

  Analise os eventos.

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

Os metadados de ID3 usam o mesmo ouvinte onTimedMetadata para indicar a presença de uma tag de ID3. No entanto, isso não deve causar confusão, pois você pode usar um `TimedMetadata` do objeto `type` para diferenciar entre TAG e ID3. Para obter mais informações sobre tags ID3, consulte [Tags ID3](../../../tvsdk-1.4-for-android/notification-system/android-1.4-id3-metadata-retrieve.md).
