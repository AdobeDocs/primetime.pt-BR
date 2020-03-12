---
description: Para receber notificações sobre tags no manifesto, é necessário implementar os ouvintes de evento apropriados.
seo-description: Para receber notificações sobre tags no manifesto, é necessário implementar os ouvintes de evento apropriados.
seo-title: Adicionar ouvintes para notificações de metadados cronometrados
title: Adicionar ouvintes para notificações de metadados cronometrados
uuid: bb996b4a-282e-4321-a9e9-513f0df45b70
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, é necessário implementar os ouvintes de evento apropriados.

Você pode monitorar metadados cronometrados ao acompanhar `onTimedMetadata`, que notificam sua aplicação de atividades relacionadas. Cada vez que uma tag assinada exclusiva é identificada durante a análise do conteúdo, o TVSDK prepara um novo `TimedMetadata` objeto e despacha esse evento. O objeto contém o nome da tag na qual você se inscreveu, a hora local na reprodução em que essa tag será exibida e outros dados.

Ouça os eventos.

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

Os metadados ID3 usam o mesmo `onTimedMetadata` ouvinte para indicar a presença de uma tag ID3. No entanto, isso não deve causar confusão, pois você pode usar a `TimedMetadata` `type` propriedade para diferenciar entre TAG e ID3. Para obter mais informações sobre tags ID3, consulte tags [](../../../../tvsdk-3x-android-prog/android-3x-content-playback-options-android2/android-3x-id3-metadata-retrieve.md)ID3.