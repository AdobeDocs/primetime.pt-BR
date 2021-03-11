---
description: A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância de Metadados.
title: Classe TimeRangeCollection
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 0%

---


# Classe TimeRangeCollection{#timerangecollection-class}

A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância de Metadados.

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

O parâmetro `type`, que é o primeiro parâmetro posicional na assinatura dos métodos do construtor, é uma instância da enumeração `TimeRangeCollection#Type`. Isso faz parte da classe `TimeRangeCollection`. Os valores atualmente definidos por essa enumeração são `MARK_RANGES`, `DELETE_RANGES` e `REPLACE_RANGES`. Você pode criar objetos `TimeRangeCollection` usando esses três tipos.
