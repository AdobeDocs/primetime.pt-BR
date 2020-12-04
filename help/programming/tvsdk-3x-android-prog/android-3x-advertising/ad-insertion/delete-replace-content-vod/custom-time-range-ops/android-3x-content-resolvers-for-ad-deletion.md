---
description: Você pode usar vários resolvedores de conteúdo para lidar com diferentes operações de linha do tempo.
seo-description: Você pode usar vários resolvedores de conteúdo para lidar com diferentes operações de linha do tempo.
seo-title: Resolvedores de conteúdo para exclusão de anúncios/substituição
title: Resolvedores de conteúdo para exclusão de anúncios/substituição
uuid: d43d54be-e04a-49dd-a695-e4e8f981ccb4
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '51'
ht-degree: 0%

---


# Resolvedores de conteúdo para exclusão de anúncio / substituição {#content-resolvers-for-ad-deletion-replacement}

Você pode usar vários resolvedores de conteúdo para lidar com diferentes operações de linha do tempo.

```java
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { 
    List<ContentResolver> resolvers = new ArrayList<ContentResolver>(); 
    MediaPlayerItemConfig itemConfig = item.getConfig(); 
    if(itemConfig) { 
        CustomRangeMetadata customRanges = itemConfig.getCustomRangeMetadata(); 
        if (customRanges) { 
            List<ReplaceTimeRange> timeRanges = customRanges.getTimeRangeList(); 
 
            if (timeRanges && timeRanges.size() > 0) { 
                //CustomRangeResolver is activated by the presence of CustomRanges 
                resolvers.add(new CustomRangeResolver()); 
            } 
        } 
        AdvertisingMetadata metadata = itemConfig.getAdvertisingMetadata(); 
        if (metadata) { 
            if (metadata instanceOf AuditudeSettings)  
            resolvers.add(new AuditudeResolver(getContext());                                      
        } 
    } 
    //Add your custom resolver if any 
    resolvers.add(MyOpportunityGenerator(item)); 
    return resolvers; 
} 
```
