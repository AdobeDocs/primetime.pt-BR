---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.
title: Tratamento de erros de exclusão e substituição de anúncios
exl-id: 86970989-82e0-4e6f-81fb-beee70870c69
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Tratamento de erros de exclusão e substituição de anúncios {#ad-deletion-and-replacement-error-handling}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico, mesclando ou reorganizando os intervalos de tempo definidos incorretamente.

O TVSDK lida com `timeRanges` erros ao fazer mesclagem e reordenação padrão. Primeiro, ele classifica intervalos de tempo definidos pelo cliente pela variável *start* hora. Com base nessa ordem de classificação, ele mescla intervalos adjacentes e os une se houver subconjuntos e interseções entre os intervalos.

O TVSDK lida com erros de intervalo de tempo da seguinte maneira:

* Fora de ordem - O TVSDK reorganiza os intervalos de tempo.
* Subconjunto - O TVSDK mescla os subconjuntos de intervalo de tempo.
* Interseção - O TVSDK mescla os intervalos de tempo de interseção.
* Conflito de intervalos de substituição - O TVSDK escolhe a duração de substituição da primeira vez que aparece `timeRange` no grupo em conflito.

O TVSDK trata os conflitos do modo de sinalização da seguinte maneira:

* Se os intervalos REPLACE forem definidos, o TVSDK alterará automaticamente o modo de sinalização para CUSTOM_RANGE.
* Se os intervalos DELETE ou MARK estiverem definidos e o modo de sinalização for CUSTOM_RANGE, o TVSDK excluirá ou marcará esses intervalos. Não há inserção de anúncio nesse caso.
* Se um intervalo DELETE ou MARK definir uma duração de substituição, o TVSDK ignorará essa duração.

Quando o servidor não retornar válido `AdBreaks`:

* O TVSDK gera e processa um `NOPTimelineOperation` para o vazio `AdBreak`. Nenhum anúncio é reproduzido.

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
