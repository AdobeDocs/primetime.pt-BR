---
description: A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações de TimeRange e fornece serviços para traduzir a si mesma em uma instância de metadados.
title: classe TimeRangeCollection
exl-id: 1af41267-c222-43ac-84ca-0bf37b6a59de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---

# classe TimeRangeCollection{#timerangecollection-class}

A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações de TimeRange e fornece serviços para traduzir a si mesma em uma instância de metadados.

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

A variável `type` o parâmetro, que é o primeiro parâmetro posicional na assinatura dos métodos do construtor, é uma instância de `TimeRangeCollection#Type` lista discriminada. Isso faz parte do `TimeRangeCollection` classe. Os valores atualmente definidos por essa lista discriminada são `MARK_RANGES`, `DELETE_RANGES`, e `REPLACE_RANGES`. Você pode criar `TimeRangeCollection` objetos que usam esses três tipos.
