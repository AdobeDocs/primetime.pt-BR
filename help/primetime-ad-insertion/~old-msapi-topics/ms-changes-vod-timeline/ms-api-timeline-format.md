---
description: Você pode especificar ou substituir linhas do tempo de ad breaks no conteúdo de VOD usando uma lista formatada de segmentos de anúncio e conteúdo chamados pods.
title: Formato da linha do tempo de VOD
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '163'
ht-degree: 0%

---


# Formato da linha do tempo de VOD {#vod-timeline-format}

Você pode especificar ou substituir linhas do tempo de ad breaks no conteúdo de VOD usando uma lista formatada de segmentos de anúncio e conteúdo chamados pods.

## Pods {#section_606E9456E25E41C8B8537A023DDD96CE}

Um pod é um ad break ou um segmento de conteúdo. Uma linha do tempo consiste em uma sequência de pods, separados por ponto e vírgula. Existem os seguintes tipos de pods:

### Intervalo comercial

```
B,duration,maximum_number_of_ads,position
```

A duração é em segundos, com precisão de 0,001 (milissegundos); o número de anúncios é um número inteiro. A posição é uma das seguintes: * **n** Nenhum — nenhum anúncio * **p** Antes da exibição — antes do conteúdo * **m** Durante a exibição — no conteúdo * **t** Pós-implantação — após o conteúdo

Por exemplo, `B,60,2,p` representa um intervalo de um minuto para até dois anúncios antes do conteúdo.

### Segmento de conteúdo - capítulo

```
C,duration,number_of_lots
```

A duração é em segundos, com precisão de 0,001 (milissegundos); o número de lotes (seções de conteúdo) é um número inteiro. Por exemplo, `C,300,1` representa uma única seção de conteúdo de cinco minutos.