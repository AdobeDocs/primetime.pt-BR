---
description: O TVSDK fornece uma experiência semelhante à da TV ao poder participar no meio de um anúncio, em transmissões ao vivo.
title: Inserção parcial de ad break
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Inserção parcial de ad break{#partial-ad-break-insertion}

O TVSDK fornece uma experiência semelhante à da TV ao poder participar no meio de um anúncio, em transmissões ao vivo.

O recurso de inserção parcial de ad-break permite imitar uma experiência semelhante à de uma TV, na qual, se o cliente iniciar um stream ao vivo dentro de um mid-roll, ele começará a ser reproduzido dentro desse mid-roll. É como mudar para um canal de TV e os comerciais rodam perfeitamente.

Por exemplo, se um usuário ingressar no meio de um ad break de 90 segundos (três anúncios de 30 segundos), 10 segundos no segundo anúncio (ou seja, aos 40 segundos do ad break), o segundo anúncio é reproduzido pela duração restante (20 segundos) seguido pelo terceiro anúncio.

## Rastrear anúncio {#section_03AFAEAA8DA44399952DC51C5E12951E}

Os rastreadores de anúncios do anúncio parcialmente reproduzido (o segundo anúncio) não são acionados. No exemplo acima, somente o rastreador do terceiro anúncio é acionado.

## Comportamento com antes da exibição {#section_7DFBFB12E63343D1A0C614F0CF9F1714}

O recurso funciona quando um anúncio precedente é reproduzido com conteúdo em tempo real. O fluxo é reproduzido a partir do ponto ativo após o fim do anúncio precedente.

Os eventos de ad break são enviados mesmo se não houver anúncios completos nesse ad break. Um anúncio é considerado um anúncio parcial, se for ignorado por mais de um segundo. Por exemplo, se um visualizador assistir a um anúncio ignorado por 800 ms, ele será considerado um anúncio completo.
