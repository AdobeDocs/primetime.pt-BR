---
description: Para receber notificações sobre tags no manifesto, é necessário implementar os ouvintes de eventos apropriados.
title: Adicionar ouvintes para notificações de metadados cronometrados
exl-id: e4be34b6-0f29-45b8-a089-b79b41daeada
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 0%

---

# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, é necessário implementar os ouvintes de eventos apropriados.

Você pode monitorar metadados cronometrados ouvindo `onTimedMetadata`, que notificam sua aplicação sobre atividades relacionadas. Cada vez que uma tag única assinada é identificada durante a análise do conteúdo, o TVSDK prepara uma nova `TimedMetadata` e despacha esse evento. O objeto contém o nome da tag que você assinou, o horário local na reprodução em que essa tag aparecerá e outros dados.

Analise os eventos.

```java
private final TimedMetadataEventListener timedMetadataEventListener = new TimedMetadataEventListener() { 
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
        } else if (_mediaPlayer.getPlaybackRange() != null && _mediaPlayer.getPlaybackRange().getDuration() > 0) { 
            displayRanges(); 
        } 
    } 
}; 
```

Os metadados de ID3 usam o mesmo `onTimedMetadata` ouvinte para indicar a presença de uma tag ID3. No entanto, isso não deve causar confusão, pois você pode usar o `TimedMetadata` `type` para diferenciar entre TAG e ID3. Para obter mais informações sobre tags ID3, consulte [Tags ID3](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md).
