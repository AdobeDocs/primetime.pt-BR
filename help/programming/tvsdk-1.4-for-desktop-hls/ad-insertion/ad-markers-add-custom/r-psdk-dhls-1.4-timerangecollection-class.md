---
description: A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações de TimeRange e fornece serviços para traduzir a si mesma em uma instância de metadados.
title: classe TimeRangeCollection
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '70'
ht-degree: 0%

---

# classe TimeRangeCollection{#timerangecollection-class}

A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações de TimeRange e fornece serviços para traduzir a si mesma em uma instância de metadados.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

O valor definido para o tipo de coleção é `MARK_RANGES`, `DELETE_RANGES`, e `REPLACE_RANGES`. Você pode criar `TimeRangeCollection`O está usando esses três tipos.
