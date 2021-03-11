---
description: Os marcadores de anúncios personalizados permitem que você transmita um conjunto de especificações de Intervalo de tempo que representam segmentos de linha do tempo para o TVSDK.
title: Classe TimeRange
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---


# Classe TimeRange{#timerange-class}

Os marcadores de anúncios personalizados permitem que você transmita um conjunto de especificações de Intervalo de tempo que representam segmentos de linha do tempo para o TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada especificação de TimeRange no conjunto representa um segmento na linha do tempo de reprodução que é mantido internamente pelo TVSDK e que deve ser marcado adequadamente como um período relacionado a anúncios.

A classe `TimeRange` é uma estrutura de dados simples que expõe a posição inicial e final na linha do tempo. Essas duas propriedades somente leitura abstraindo a ideia de um intervalo de tempo na linha do tempo da reprodução.

>[!TIP]
>
>Ambos os valores são expressos em milissegundos.

Aqui está um resumo da classe `TimeRange`:

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

