---
description: A classe de utilitário ReplaceTimeRange é uma extensão da classe TimeRange a ser usada com CustomRangeMetadata.
title: classe ReplaceTimeRange
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '36'
ht-degree: 0%

---

# classe ReplaceTimeRange {#replacetimerange-class}

A classe de utilitário ReplaceTimeRange é uma extensão da classe TimeRange a ser usada com CustomRangeMetadata.

```java
public class ReplaceTimeRange extends TimeRange {
    // Default constructor method
    public ReplaceTimeRange() { 
        ... 
    }

    // Details of begining, duration and replaceDuration 
    // provided at construction time 
    public ReplaceTimeRange(long begin, long duration, long replaceDuration) { 
        ... 
    }

    // Replace duration
    public long getReplaceDuration() { 
        ... 
    }
}
```
