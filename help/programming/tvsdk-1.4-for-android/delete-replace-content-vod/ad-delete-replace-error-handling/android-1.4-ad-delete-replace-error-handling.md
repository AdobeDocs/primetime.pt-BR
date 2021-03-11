---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.
title: Exclusão de anúncios e tratamento de erros de substituição
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---


# Exclusão de anúncio e tratamento de erros de substituição{#ad-deletion-and-replacement-error-handling}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.

O TVSDK lida com erros `timeRanges` ao fazer a mesclagem e a reordenação padrão. Primeiro, ele classifica os intervalos de tempo definidos pelo cliente de acordo com a hora *begin*. Com base nessa ordem de classificação, ela mescla intervalos adjacentes e os une se houver subconjuntos e interseções entre os intervalos.

O TVSDK trata os erros de intervalo de tempo da seguinte maneira:

* Fora de ordem - O TVSDK reorganiza os intervalos de tempo.
* Subconjunto - O TVSDK mescla os subconjuntos de intervalo de tempo.
* Interseção - O TVSDK mescla os intervalos de tempo de interseção.
* Substituir conflito de intervalos - O TVSDK escolhe a duração da substituição do mais antigo que aparece `timeRange` no grupo em conflito.

O TVSDK lida com conflitos do modo de sinalização com metadados de anúncio da seguinte maneira:

* Se o modo de sinalização do anúncio estiver em conflito com os metadados do intervalo de tempo, os metadados do intervalo de tempo sempre terão prioridade. Por exemplo, se o modo de sinalização do anúncio estiver definido como mapa do servidor ou dicas de manifesto e também houver intervalos de tempo MARK nos metadados do anúncio, o comportamento resultante será que os intervalos estão marcados e nenhum anúncio será inserido.
* Para intervalos REPLACE, se o modo de sinalização estiver definido como mapa do servidor ou dicas de manifesto, os intervalos serão substituídos conforme especificado nos intervalos REPLACE e não haverá inserção de anúncio por meio de mapa do servidor ou dicas de manifesto. Consulte [Modo de sinalização de anúncio](../../../tvsdk-1.4-for-android/ad-insertion/ad-insertion-metadata/android-1.4-ad-signaling-mode.md).

Quando o servidor não retorna um `AdBreaks` válido:

* O TVSDK gera e processa um `NOPTimelineOperation` para o `AdBreak` vazio. Nenhuma reprodução de anúncio.

Para intervalos de tempo com fluxos ao vivo:

* Embora esse recurso de exclusão/substituição de anúncio C3 deva ser suportado apenas para VOD, os intervalos de tempo são processados para fluxos ao vivo, bem como se especificado nos metadados do anúncio.

## Exemplos de erro de intervalo de tempo {#time-range-error-examples}

O TVSDK responde a especificações de intervalo de tempo incorretas ao mesclar ou substituir os intervalos de tempo, conforme apropriado.

No exemplo a seguir, quatro intervalos de tempo de DELETE de interseção são definidos. O TVSDK mescla os quatro intervalos de tempo em um, para que o intervalo de exclusão real seja de 0 a 50.

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

No exemplo a seguir, quatro intervalos de tempo REPLACE são definidos com intervalos de tempo conflitantes. Nesse caso, o TVSDK substitui de 0 a 50s por 25s de anúncios. Ele vai com a primeira duração de substituição na ordem de classificação, porque há conflitos em intervalos subsequentes.

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
