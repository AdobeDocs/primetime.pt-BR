---
description: A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância de Metadados.
title: Classe TimeRangeCollection
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---


# Classe TimeRangeCollection{#timerangecollection-class}

A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância de Metadados.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

O valor definido para o tipo de coleção é `MARK_RANGES`, `DELETE_RANGES` e `REPLACE_RANGES`. Você pode criar `TimeRangeCollection`s usando esses três tipos.
