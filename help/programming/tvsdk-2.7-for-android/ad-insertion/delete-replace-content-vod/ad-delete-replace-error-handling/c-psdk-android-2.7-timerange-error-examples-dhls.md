---
description: O TVSDK responde a especificações de intervalo de tempo incorretas mesclando ou substituindo os intervalos de tempo conforme apropriado.
title: Exemplos de erro de intervalo de tempo
exl-id: 70bbd98b-4084-4a26-8420-fdbe9029194d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# Exemplos de erro de intervalo de tempo{#time-range-error-examples}

O TVSDK responde a especificações de intervalo de tempo incorretas mesclando ou substituindo os intervalos de tempo conforme apropriado.

**Intervalo de tempo DELETE**

No exemplo a seguir, quatro intervalos de tempo de DELETE de interseção são definidos. O TVSDK mescla os quatro intervalos de tempo em um, para que o intervalo de exclusão real seja de 0 a 50 s.

```
"time-ranges": {
    "type": "delete",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000
        },
        {
            "begin": 20000,
            "end": 50000
        },
        {
            "begin": 0,
            "end": 30000
        },
        {
            "begin": 30000,
            "end": 40000
        }
    ]
}
```

**SUBSTITUIR intervalo de tempo**

No exemplo a seguir, quatro intervalos de tempo REPLACE são definidos com intervalos de tempo conflitantes. Nesse caso, o TVSDK substitui de 0 a 50 por 25 segundos de anúncios. Acompanha a primeira duração de substituição na ordem de classificação, pois há conflitos nos intervalos subsequentes.

```
"time-ranges": {
    "type": "replace",
    "time-range-list": [
        {
            "begin": 10000,
            "end": 35000,
            "replace-duration": 15000
        },
        {
            "begin": 20000,
            "end": 50000,
            "replace-duration": 20000
        },
        {
            "begin": 0,
            "end": 30000,
            "replace-duration": 25000
        },
        {
            "begin": 30000,
            "end": 40000,
            "replace-duration": 30000
        }
    ]
}
```
