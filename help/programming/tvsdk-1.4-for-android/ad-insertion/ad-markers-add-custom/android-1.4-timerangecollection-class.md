---
description: A classe do utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância Metadata.
seo-description: A classe do utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância Metadata.
seo-title: classe TimeRangeCollection
title: classe TimeRangeCollection
uuid: 5705dc9d-4325-44b0-b5aa-196d09c3a67e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '124'
ht-degree: 0%

---


# Classe TimeRangeCollection{#timerangecollection-class}

A classe do utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância Metadata.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```java
public final class TimeRangeCollection {
    // default constructor method
    public TimeRangeCollection(Type type) {...}

    // the list of timerange specifications provided at construction time 
    public TimeRangeCollection(Type type, List<TimeRange> timeRanges) {...}

    // timerange specs can also be added later
    public void addTimeRange(TimeRange timeRange) {...}

    // translate the set of timerange specs into a Metadata instance 
    public Metadata toMetadata(Metadata options) {...}
}
```

O parâmetro `type`, que é o primeiro parâmetro posicional na assinatura dos métodos do construtor, é uma instância da lista discriminada `TimeRangeCollection#Type`. Isso faz parte da classe `TimeRangeCollection`. Os valores atualmente definidos por essa lista discriminada são `MARK_RANGES`, `DELETE_RANGES` e `REPLACE_RANGES`. Você pode criar `TimeRangeCollection` objetos usando esses três tipos.
