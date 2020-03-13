---
description: Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.
seo-description: Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.
seo-title: classe TimeRange
title: classe TimeRange
uuid: 5d0c979e-cc63-4fdd-becc-b0e3987b0891
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# classe TimeRange{#timerange-class}

Os marcadores de anúncio personalizados permitem que você passe um conjunto de especificações TimeRange que representam segmentos de linha do tempo para TVSDK.

<!--<a id="section_42EB6D62627A424ABA250E3246EFEFC3"></a>-->

Cada especificação no conjunto representa um segmento na linha do tempo de reprodução mantido internamente pelo TVSDK e que deve ser marcado adequadamente como um período relacionado a anúncios. `TimeRange`

A `TimeRange` classe é uma estrutura de dados simples que expõe a posição inicial e final na linha do tempo. Essas duas propriedades somente leitura abstrairão a ideia de um intervalo de tempo na linha do tempo de reprodução.

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

