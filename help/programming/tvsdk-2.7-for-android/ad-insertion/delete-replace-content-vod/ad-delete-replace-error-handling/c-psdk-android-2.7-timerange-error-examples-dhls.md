---
description: O TVSDK responde a especificações de intervalo de tempo incorretas ao mesclar ou substituir os intervalos de tempo, conforme apropriado.
seo-description: O TVSDK responde a especificações de intervalo de tempo incorretas ao mesclar ou substituir os intervalos de tempo, conforme apropriado.
seo-title: Exemplos de erros de intervalo de tempo
title: Exemplos de erros de intervalo de tempo
uuid: f6cc1e61-8f42-4559-b643-2134180a8c5e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Exemplos de erros de intervalo de tempo{#time-range-error-examples}

O TVSDK responde a especificações de intervalo de tempo incorretas ao mesclar ou substituir os intervalos de tempo, conforme apropriado.

**EXCLUIR intervalo de tempo**

No exemplo a seguir, quatro intervalos de tempo de interseção DELETE são definidos. O TVSDK mescla os quatro intervalos de tempo em um, para que o intervalo de exclusão real seja de 0 a 50 s.

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

No exemplo a seguir, quatro intervalos de tempo REPLACE são definidos com intervalos de tempo conflitantes. Nesse caso, o TVSDK substitui de 0 a 50 s por 25 s de anúncios. Ele vai com a primeira duração de substituição na ordem de classificação, porque há conflitos em intervalos subsequentes.

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

