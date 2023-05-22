---
description: Os marcadores de anúncios personalizados permitem passar um conjunto de especificações de Intervalo de tempo que representam segmentos da linha do tempo para o TVSDK.
title: classe TimeRange
exl-id: f86dee89-15de-4caa-b05c-3e08516b32ce
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# classe TimeRange {#timerange-class}

Os marcadores de anúncios personalizados permitem passar um conjunto de especificações de Intervalo de tempo que representam segmentos da linha do tempo para o TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Each `TimeRange` A especificação no conjunto representa um segmento na linha do tempo de reprodução que é mantido internamente pelo TVSDK e que deve ser marcado apropriadamente como um período relacionado a anúncios.

A variável `TimeRange` class é uma estrutura de dados simples que expõe a posição inicial e a posição final na linha do tempo. Essas duas propriedades somente leitura abstraem a ideia de um intervalo de tempo na linha do tempo de reprodução.

>[!TIP]
>
>Ambos os valores são expressos em milissegundos.

Aqui está um resumo da `TimeRange` classe:

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
