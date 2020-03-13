---
description: A classe do utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância Metadata.
seo-description: A classe do utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância Metadata.
seo-title: classe TimeRangeCollection
title: classe TimeRangeCollection
uuid: da781df4-6b19-47e1-8dc5-ea83c139f061
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# classe TimeRangeCollection{#timerangecollection-class}

A classe do utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações TimeRange e fornece serviços para se traduzir em uma instância Metadata.

<!--<a id="section_D87AA7BC628D458DAB12D5247AD34B41"></a>-->

```
public final class TimeRangeCollection { 
    public static const MARK_RANGES:String = "mark_ranges"; 
  
    public function TimeRangeCollection(timeRanges:Vector.<TimeRange>) {…} 
    public function addTimeRange(timeRange:TimeRange):void {…} 
    public function toMetadata(options:Metadata):Metadata {…} 
}
```

O valor definido para o tipo de coleção é `MARK_RANGES`, `DELETE_RANGES`e `REPLACE_RANGES`. Você pode criar `TimeRangeCollection`s usando esses três tipos.
