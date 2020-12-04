---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.
seo-description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.
seo-title: Tratamento de erros de exclusão e substituição de anúncios
title: Tratamento de erros de exclusão e substituição de anúncios
uuid: ab153591-0011-44b4-87f9-be0302c2295e
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 0%

---


# Exclusão de anúncios e tratamento de erros de substituição {#ad-deletion-and-replacement-error-handling}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.

O TVSDK lida com `timeRanges` erros ao realizar a mesclagem padrão e a reorganização. Primeiro, ele classifica os intervalos de tempo definidos pelo cliente de acordo com a hora *begin*. Com base nessa ordem de classificação, ela mescla intervalos adjacentes e os une se houver subconjuntos e interseções entre os intervalos.

O TVSDK lida com erros de intervalo de tempo da seguinte maneira:

* Fora de ordem - O TVSDK reorganiza os intervalos de tempo.
* Subconjunto - O TVSDK mescla os subconjuntos de intervalo de tempo.
* Interseção - o TVSDK mescla os intervalos de tempo de interseção.
* Substituir conflito de intervalos - o TVSDK escolhe a duração da substituição do mais antigo `timeRange` no grupo em conflito.

O TVSDK lida com conflitos de modo de sinalização da seguinte maneira:

* Se os intervalos REPLACE estiverem definidos, o TVSDK altera automaticamente o modo de sinalização para CUSTOM_RANGE.
* Se os intervalos de DELETE ou MARK estiverem definidos e o modo de sinalização for CUSTOM_RANGE, o TVSDK excluirá ou marcará esses intervalos. Nesse caso, não há inserção de anúncio.
* Se um intervalo de DELETE ou um intervalo MARK definir uma duração de substituição, o TVSDK ignorará essa duração.

Quando o servidor não retornar válido `AdBreaks`:

* O TVSDK gera e processa um `NOPTimelineOperation` para o `AdBreak` vazio. Nenhum anúncio é reproduzido.

## Exemplos de erro de intervalo de tempo {#time-range-error-examples}

O TVSDK responde a especificações de intervalo de tempo incorretas ao mesclar ou substituir os intervalos de tempo, conforme apropriado.

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

No exemplo a seguir, quatro intervalos de tempo REPLACE são definidos com intervalos de tempo conflitantes. Nesse caso, o TVSDK substitui de 0 a 50 s por 25 s de anúncios. Ele vai com a primeira duração de substituição na ordem de classificação, porque há conflitos em intervalos subsequentes.

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
