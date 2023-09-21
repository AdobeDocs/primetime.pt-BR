---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.
title: Tratamento de erros de exclusão e substituição de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Tratamento de erros de exclusão e substituição de anúncios{#ad-deletion-and-replacement-error-handling}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.

O TVSDK lida com `timeRanges` erros ao fazer mesclagem e reordenação padrão. Primeiro, ele classifica intervalos de tempo definidos pelo cliente pela variável *start* hora. Com base nessa ordem de classificação, ele mescla intervalos adjacentes e os une se houver subconjuntos e interseções entre os intervalos.

O TVSDK lida com erros de intervalo de tempo da seguinte maneira:

* Fora de ordem - O TVSDK reorganiza os intervalos de tempo.
* Subconjunto - O TVSDK mescla os subconjuntos de intervalo de tempo.
* Interseção - O TVSDK mescla os intervalos de tempo de interseção.
* Conflito de intervalos de substituição - O TVSDK escolhe a duração de substituição da primeira vez que aparece `timeRange` no grupo em conflito.

O TVSDK lida com conflitos do modo de sinalização com metadados de anúncio da seguinte maneira:

* Se o modo de sinalização de anúncios entrar em conflito com os metadados de intervalo de tempo, os metadados de intervalo de tempo sempre terão prioridade. Por exemplo, se o modo de sinalização de anúncios estiver definido como mapa do servidor ou dicas de manifesto e também houver intervalos de tempo MARCAR nos metadados de anúncios, o comportamento resultante será que os intervalos estão marcados e nenhum anúncio foi inserido.
* Para intervalos REPLACE, se o modo de sinalização estiver definido como mapa do servidor ou sinalização de manifesto, os intervalos serão substituídos conforme especificado nos intervalos REPLACE e não haverá inserção de anúncio por meio do mapa do servidor ou sinalização de manifesto. Consulte [Modo de sinalização de anúncios](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

Quando o servidor não retornar válido `AdBreaks`:

* O TVSDK gera e processa um `NOPTimelineOperation` para o vazio `AdBreak`. Nenhum anúncio é reproduzido.

Para intervalos de tempo com transmissões em tempo real:

* Embora esse recurso de exclusão/substituição de anúncios C3 seja destinado a ser compatível apenas com VOD, os intervalos de tempo são processados para transmissões em tempo real, bem como se especificados nos metadados de anúncios.

## Exemplos de erro de intervalo de tempo {#time-range-error-examples}

O TVSDK responde a especificações de intervalo de tempo incorretas mesclando ou substituindo os intervalos de tempo conforme apropriado.

No exemplo a seguir, quatro intervalos de tempo de DELETE de interseção são definidos. O TVSDK mescla os quatro intervalos de tempo em um, para que o intervalo de exclusão real seja de 0 a 50 s.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000
    }, {
        "begin": 20000,
        "end": 50000
    }, {
        "begin": 0,
        "end": 30000
    }, {
        "begin": 30000,
        "end": 40000
    } ]
}
```

No exemplo a seguir, quatro intervalos de tempo REPLACE são definidos com intervalos de tempo conflitantes. Nesse caso, o TVSDK substitui de 0 a 50 por 25 segundos de anúncios. Acompanha a primeira duração de substituição na ordem de classificação, pois há conflitos nos intervalos subsequentes.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [ {
        "begin": 10000,
        "end": 35000,
        "replace-duration": 15000
    }, {
        "begin": 20000,
        "end": 50000,
        "replace-duration": 20000
    }, {
        "begin": 0,
        "end": 30000,
        "replace-duration": 25000
    }, {
        "begin": 30000,
        "end": 40000,
        "replace-duration": 30000
    } ]
}
```
