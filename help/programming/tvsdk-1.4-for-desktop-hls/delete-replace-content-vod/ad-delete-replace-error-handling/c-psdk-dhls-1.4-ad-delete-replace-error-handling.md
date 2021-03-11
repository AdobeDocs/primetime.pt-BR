---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.
title: Exclusão de anúncios e tratamento de erros de substituição
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---


# Erro de exclusão e substituição de anúncio que manipula {#ad-deletion-and-replacement-error-handling}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.

O TVSDK lida com erros `timeRanges` ao fazer a mesclagem e a reordenação padrão. Primeiro, ele classifica os intervalos de tempo definidos pelo cliente de acordo com a hora *begin*. Com base nessa ordem de classificação, ela mescla intervalos adjacentes e os une se houver subconjuntos e interseções entre os intervalos.

O TVSDK trata os erros de intervalo de tempo da seguinte maneira:

* Fora de ordem - O TVSDK reorganiza os intervalos de tempo.
* Subconjunto - O TVSDK mescla os subconjuntos de intervalo de tempo.
* Interseção - O TVSDK mescla os intervalos de tempo de interseção.
* Substituir conflito de intervalos - O TVSDK escolhe a duração da substituição do mais antigo que aparece `timeRange` no grupo em conflito.

O TVSDK lida com conflitos de modo de sinalização da seguinte maneira:

* Se os intervalos SUBSTITUIR forem definidos, o TVSDK alterará automaticamente o modo de sinalização para CUSTOM_RANGE.
* Se os intervalos de DELETE ou os intervalos MARK forem definidos e o modo de sinalização for CUSTOM_RANGE, o TVSDK excluirá ou marcará esses intervalos. Nesse caso, não há inserção de anúncio.
* Se um intervalo de DELETE ou um intervalo MARK definir uma duração de substituição, o TVSDK ignorará essa duração.

Quando o servidor não retorna um `AdBreaks` válido:

* O TVSDK gera e processa um `NOPTimelineOperation` para o `AdBreak` vazio. Nenhuma reprodução de anúncio.

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
