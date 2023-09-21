---
description: Os marcadores de anúncios personalizados permitem passar um conjunto de especificações de Intervalo de tempo que representam segmentos da linha do tempo para o TVSDK.
title: classe TimeRange
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# classe TimeRange{#timerange-class}

Os marcadores de anúncios personalizados permitem passar um conjunto de especificações de Intervalo de tempo que representam segmentos da linha do tempo para o TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Each `TimeRange` A especificação no conjunto representa um segmento na linha do tempo de reprodução que é mantido internamente pelo TVSDK e que deve ser marcado apropriadamente como um período relacionado a anúncios.

A variável `TimeRange` class é uma estrutura de dados simples que expõe a posição inicial e a posição final na linha do tempo. Essas duas propriedades somente leitura abstraem a ideia de um intervalo de tempo na linha do tempo de reprodução.

>[!TIP]
>
>Ambos os valores são expressos em milissegundos.

Este é um resumo da classe TimeRange:

```
public final class TimeRange {
    // the start/end values are provided at construction 
    public static function createRange(begin:Number, duration:Number {…}
 
    public function get begin():Number {…}
    public function get end():Number {…}
    public function get duration():Number {…}
}
```
