---
description: Você pode usar vários resolvedores de conteúdo para lidar com diferentes operações de linha do tempo.
title: Resolvedores de conteúdo para exclusão/substituição de anúncios
exl-id: 67677d12-a3a6-4fac-8704-441b81cb10fe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '34'
ht-degree: 0%

---

# Resolvedores de conteúdo para exclusão/substituição de anúncios {#content-resolvers-for-ad-deletion-replacement}

Você pode usar vários resolvedores de conteúdo para lidar com diferentes operações de linha do tempo.

```java
List<ContentResolver> contentResolvers = new ArrayList<ContentResolver>(); 
MetadataNode metadata = (MetadataNode) resource.getMetadata(); 
if (metadata != null) { 
    if (metadata.containsKey(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue())) { 
        String timeRangeType = metadata.getValue(DefaultMetadataKeys.TIME_RANGES_METADATA_KEY.getValue()); 
        if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_DELETE)) { 
            contentResolvers.add(new DeleteContentResolver()); 
        } else if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_REPLACE)) { 
            contentResolvers.add(new DeleteContentResolver()); 
        } else if (timeRangeType.equals(TimeRangeCollection.TIME_RANGE_TYPE_MARK)) { 
            contentResolvers.add(new CustomAdMarkersContentResolver()); 
        } 
    } 
    if (metadata.containsKey(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue())) { 
        contentResolvers.add(new AuditudeResolver(context)); 
    } else if (metadata.containsKey(DefaultMetadataKeys.JSON_METADATA_KEY.getValue())) { 
        contentResolvers.add(new MetadataResolver()); 
    } 
} 
return contentResolvers;
```
