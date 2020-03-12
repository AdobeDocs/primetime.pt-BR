---
description: A classe do utilitário ReplaceTimeRange é uma extensão da classe TimeRange a ser usada com CustomRangeMetadata.
seo-description: A classe do utilitário ReplaceTimeRange é uma extensão da classe TimeRange a ser usada com CustomRangeMetadata.
seo-title: Classe ReplaceTimeRange
title: Classe ReplaceTimeRange
uuid: 19c49b26-5096-4429-b30b-bdd2502e3036
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Classe ReplaceTimeRange {#replacetimerange-class}

A classe do utilitário ReplaceTimeRange é uma extensão da classe TimeRange a ser usada com CustomRangeMetadata.

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

