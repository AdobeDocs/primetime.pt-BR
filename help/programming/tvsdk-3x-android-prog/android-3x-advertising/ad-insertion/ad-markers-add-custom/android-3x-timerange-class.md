---
description: Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.
seo-description: Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.
seo-title: classe TimeRange
title: classe TimeRange
uuid: af3ce5e6-44b5-457f-a6e7-aa232defb91e
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# classe TimeRange {#timerange-class}

Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada especificação no conjunto representa um segmento na linha do tempo de reprodução mantido internamente pelo TVSDK e que deve ser marcado adequadamente como um período relacionado a anúncios. `TimeRange`

A `TimeRange` classe é uma estrutura de dados simples que expõe a posição inicial e final na linha do tempo. Essas duas propriedades somente leitura abstrairão a ideia de um intervalo de tempo na linha do tempo de reprodução.

>[!TIP]
>
>Ambos os valores são expressos em milissegundos.

Este é um resumo da `TimeRange` classe:

```java
public final class TimeRange {
    // the start/end values are provided at construction time
    public static TimeRange createRange(long begin, long duration) {...} 

    // only getters are available
    public long getBegin() {...} 
    public long getEnd() {...} 
    public long getDuration() {...}
}
```
