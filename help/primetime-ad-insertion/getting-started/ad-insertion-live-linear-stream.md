---
title: Usar Ad Insertion no fluxo ao vivo/linear
description: Uso do Ad Insertion no fluxo ao vivo/linear
exl-id: d56ed723-ec72-4bbd-befc-6858c7c9d800
source-git-commit: 1bc2f6c230c262babf2958c32fee31afcad04c2f
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---

# Usar Ad Insertion no fluxo ao vivo/linear {#ad-insertion-live-linear-stream}

O Primetime Ad Insertion dá aos editores a capacidade de lidar com situações padrão e complexas de inserção de anúncios que ocorrem durante fluxos dinâmicos/lineares.

## Formatos de Indicação Suportados {#cue-formats-supported}

O Primetime Ad Insertion suporta uma ampla variedade de formatos de sinalização padrão e não padrão, incluindo:

* DPI SCTE-35 (marcadores de anúncios aprimorados SCTE-35)

* [Especificação de sinalização de inserção de programa digital Adobe](assets/PrimetimeDigitalProgramInsertionSignalingSpecification.pdf)

* SCTE-35 binário (HLS e DASH)

* SCTE-35 textual (HLS e DASH)

Entre em contato com o representante de suporte do Primetime para obter detalhes adicionais ou outros formatos de sinalização compatíveis.

## Suporte a ad break parcial {#partial-ad-break-support}

Os ad breaks parciais podem ser usados em situações em que um visualizador entra em um fluxo ao vivo/linear após um ad break ser iniciado.  Por exemplo, se um visualizador insere um ad break de 2:00 na marca de 1:00, a inserção de ad break parcial garante que os anúncios sejam veiculados no tempo restante. Sem a inserção parcial de ad break, nenhum anúncio seria exibido para esse visualizador durante a interrupção. O Primetime Ad Insertion permite a inserção de ad break parcial por padrão se as tags apropriadas estiverem presentes nos fluxos de mídia.

## Retorno antecipado (saída antecipada do anúncio) {#early-return-early-ad-exit}

Há instâncias em que pode ser necessário retornar antecipadamente de um ad break em um fluxo ao vivo/linear, como quando um evento esportivo repentinamente retorna à ação. Cada formato de decisão de anúncio contém uma tag para &quot;cue-out&quot; (anúncios) ou &quot;cue-in&quot; (conteúdo).  Se uma tag de &quot;cue-in&quot; for encontrada antes do final de um ad break, o Adobe Primetime Ad Insertion respeitará a cue-in.  Entre em contato com o empacotador de conteúdo para ativar o retorno antecipado.
