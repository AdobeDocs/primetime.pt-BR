---
description: O TVSDK fornece uma experiência de TV de poder participar do meio de um anúncio, em streams ao vivo.
title: Inserção parcial de ad break
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---


# Inserção parcial de ad break{#partial-ad-break-insertion}

O TVSDK fornece uma experiência de TV de poder participar do meio de um anúncio, em streams ao vivo.

O recurso de inserção parcial de ad break permite que você imite uma experiência semelhante a uma TV, onde, se o cliente iniciar um stream ao vivo dentro de um intermediário, ele começa a reproduzir no meio da exibição. É semelhante a mudar para um canal de TV e os comerciais funcionam perfeitamente.

Por exemplo, se um usuário ingressar no meio de um ad break de 90 segundos (três anúncios de 30 segundos), 10 segundos no segundo anúncio (ou seja, 40 segundos no ad break), o segundo anúncio será reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.

## Rastrear anúncio {#section_03AFAEAA8DA44399952DC51C5E12951E}

Rastreadores de anúncios para o anúncio parcialmente reproduzido (o segundo anúncio) não são acionados. No exemplo acima, somente o rastreador do terceiro anúncio é acionado.

## Comportamento com {#section_7DFBFB12E63343D1A0C614F0CF9F1714} precedente

O recurso funciona quando um anúncio precedente é reproduzido com conteúdo ao vivo. O fluxo é reproduzido do ponto ativo após o término do anúncio precedente.

Os eventos de ad break são enviados mesmo se não houver anúncios completos neste ad break. Um anúncio é considerado um anúncio parcial, se for ignorado por mais de um segundo. Por exemplo, se um visualizador assistir um anúncio ignorado por 800 ms, ele será considerado um anúncio completo.
