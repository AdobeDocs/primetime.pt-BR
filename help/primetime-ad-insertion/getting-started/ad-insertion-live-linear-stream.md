---
title: Usar Ad Insertion no fluxo ao vivo/linear
description: Uso do Ad Insertion no fluxo ao vivo/linear
translation-type: tm+mt
source-git-commit: 0f98b9848f1764e7c66e3692d8a845513493597f
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---


# Usar Ad Insertion no fluxo ao vivo/linear {#ad-insertion-live-linear-stream}

O Primetime Ad Insertion dá aos editores a capacidade de lidar com situações padrão e complexas de inserção de anúncios que ocorrem durante fluxos ao vivo/lineares.

## Formatos de sinalização suportados {#cue-formats-supported}

O Primetime Ad Insertion suporta uma grande variedade de formatos de sinalização padrão e não padrão, incluindo:

* DPI SCTE-35 (marcadores de anúncio aprimorados SCTE-35)

* [Especificação de sinalização de inserção do Programa digital Adobe](https://www.adobe.com/content/dam/acom/en/devnet/primetime/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* SCTE-35 binário (HLS e DASH)

* SCTE-35 textual (HLS e DASH)

Entre em contato com o representante de suporte do Primetime para obter mais detalhes ou outros formatos de sinalização compatíveis.

## Suporte parcial para quebra de anúncios {#partial-ad-break-support}

Quebras parciais de anúncios podem ser usadas em situações em que um visualizador entra em um fluxo ao vivo/linear depois que uma pausa de anúncio é iniciada.  Por exemplo, se um visualizador digitar uma pausa de anúncio de 2:00 no intervalo de 1:00, a inserção parcial do anúncio garante que os anúncios serão veiculados no tempo restante. Sem a inserção parcial de um anúncio, nenhum anúncio seria veiculado para esse visualizador durante a pausa. O Primetime Ad Insertion permite a inserção parcial de anúncios por padrão se as tags apropriadas estiverem presentes nos fluxos de mídia.

## Retorno antecipado (Saída antecipada do anúncio) {#early-return-early-ad-exit}

Há casos em que pode ser necessário retornar cedo de uma pausa de anúncio em um fluxo ao vivo/linear, como quando um evento esportivo retorna à ação de repente. Cada formato de decisão de anúncio contém uma tag para &quot;cue-out&quot; (anúncios) ou &quot;cue-in&quot; (conteúdo).  Se uma tag de &quot;entrada&quot; for encontrada antes do fim de uma pausa de anúncio, o Adobe Primetime Ad Insertion honrará a entrada.  Entre em contato com seu empacotador de conteúdo para habilitar o retorno antecipado.
