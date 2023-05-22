---
description: A classe de utilitário TimeRangeCollection abstrai a noção de uma coleção ordenada de especificações de TimeRange e fornece serviços para traduzir a si mesma em uma instância de metadados.
title: classe TimeRangeCollection
exl-id: 2e5160b0-2254-4a40-8c32-fe3e05b9fc30
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
