---
description: Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.
seo-description: Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.
seo-title: classe TimeRange
title: classe TimeRange
uuid: adf4f1ad-6b3b-48ac-a388-ee1fd54f770b
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 0%

---


# Classe TimeRange{#timerange-class}

Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada especificação TimeRange no conjunto representa um segmento na linha do tempo de reprodução mantido internamente pelo TVSDK e que deve ser marcado adequadamente como um período relacionado a anúncios.

A classe `TimeRange` é uma estrutura de dados simples que expõe a posição do start e a posição final na linha do tempo. Essas duas propriedades somente leitura abstrairão a ideia de um intervalo de tempo na linha do tempo de reprodução.

>[!TIP]
>
>Ambos os valores são expressos em milissegundos.

Este é um resumo da classe `TimeRange`:

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

