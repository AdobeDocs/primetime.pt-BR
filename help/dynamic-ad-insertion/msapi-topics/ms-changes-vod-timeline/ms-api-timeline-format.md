---
description: Você pode especificar ou substituir linhas do tempo para quebras de anúncios no conteúdo VOD usando uma lista formatada de segmentos de anúncios e conteúdo chamados pods.
seo-description: Você pode especificar ou substituir linhas do tempo para quebras de anúncios no conteúdo VOD usando uma lista formatada de segmentos de anúncios e conteúdo chamados pods.
seo-title: Formato de linha do tempo VOD
title: Formato de linha do tempo VOD
uuid: 6daaf605-e5ee-48dc-a222-a5973b3d915a
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9

---


# Formato de linha do tempo VOD {#vod-timeline-format}

Você pode especificar ou substituir linhas do tempo para quebras de anúncios no conteúdo VOD usando uma lista formatada de segmentos de anúncios e conteúdo chamados pods.

## Pods {#section_606E9456E25E41C8B8537A023DDD96CE}

Um pod é uma quebra de anúncio ou um segmento de conteúdo. Uma linha do tempo consiste em uma sequência de pods, separados por ponto-e-vírgula. Os seguintes tipos de pods existem:

### Quebra de anúncio

```
B,duration,maximum_number_of_ads,position
```

A duração é em segundos, com precisão de 0,001 (milissegundos); o número de anúncios é um número inteiro. A posição é uma das seguintes:
* **n** Nenhum — no ad* **p** Pre-roll — antes do conteúdo* **m** intercalar — no conteúdo* **t** Pós-rolagem — após o conteúdo

Por exemplo, `B,60,2,p` representa uma quebra de um minuto para até duas publicidades antes do conteúdo.

### Segmento de conteúdo - capítulo

```
C,duration,number_of_lots
```

A duração é em segundos, com precisão de 0,001 (milissegundos); o número de lotes (seções de conteúdo) é um número inteiro. Por exemplo, `C,300,1` representa uma única seção de conteúdo de cinco minutos.