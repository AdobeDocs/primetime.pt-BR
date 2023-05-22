---
description: O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se o trick play é compatível e outras funcionalidades relacionadas ao avanço e retrocesso rápidos.
title: Elementos da API de alteração de taxa
exl-id: 282d0d12-5244-4abd-893a-7e3c4d2f4fe8
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---

# Elementos da API de alteração de taxa {#rate-change-api-elements}

O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se o trick play é compatível e outras funcionalidades relacionadas ao avanço e retrocesso rápidos.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Use os seguintes elementos de API para alterar as taxas de reprodução:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, que especifica taxas válidas.

| **Valor da taxa** | **Efeito na reprodução** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Muda para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Alterna para o modo de retrocesso rápido |
| 1.0 | Muda para o modo normal de reprodução (chamando `play` é o mesmo que definir a propriedade rate como 1,0) |
| 0.0 | Pausas (chamando `pause` é o mesmo que definir a propriedade rate como 0,0) |
