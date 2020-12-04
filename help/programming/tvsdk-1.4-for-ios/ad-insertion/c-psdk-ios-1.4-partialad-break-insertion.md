---
description: O TVSDK fornece uma experiência semelhante à da TV de poder participar no meio de um anúncio, em fluxos ao vivo.
seo-description: O TVSDK fornece uma experiência semelhante à da TV de poder participar no meio de um anúncio, em fluxos ao vivo.
seo-title: Inserção parcial de quebra de anúncio
title: Inserção parcial de quebra de anúncio
uuid: b6ee62da-c4d1-42f2-b03d-f73247f8e585
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---


# Inserção parcial de quebra de anúncio{#partial-ad-break-insertion}

O TVSDK fornece uma experiência semelhante à da TV de poder participar no meio de um anúncio, em fluxos ao vivo.

O recurso de inserção parcial de quebra de anúncio permite que você imite uma experiência semelhante à da TV em que, se o cliente start um fluxo ao vivo dentro de um mid-roll, ele start reproduzindo dentro desse mid-roll. É como mudar para um canal de TV e os comerciais funcionam perfeitamente.

Por exemplo, se um usuário ingressar no meio de um intervalo de 90 segundos (três anúncios de 30 segundos), 10 segundos após o segundo anúncio (ou seja, 40 segundos após o intervalo do anúncio), o segundo anúncio será reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.

## Rastrear anúncio {#section_03AFAEAA8DA44399952DC51C5E12951E}

Os rastreadores de anúncios para o anúncio parcialmente reproduzido (o segundo anúncio) não são acionados. No exemplo acima, somente o rastreador do terceiro anúncio é acionado.

## Comportamento com pre-roll {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

O recurso funciona quando um anúncio precedente é reproduzido com conteúdo em tempo real. O fluxo é reproduzido a partir do ponto ativo após o término do anúncio precedente.

Eventos de quebra de anúncio são enviados mesmo se não houver anúncios completos neste intervalo de anúncios. Um anúncio é considerado parcial, se for ignorado por mais de um segundo. Por exemplo, se um visualizador observar um anúncio ignorado por 800 ms, ele será considerado um anúncio completo.
