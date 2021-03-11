---
description: O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avançar e retroceder rapidamente.
title: Elementos da API de alteração de taxa
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 3%

---


# Alterar taxa de elementos da API {#rate-change-api-elements}

O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avançar e retroceder rapidamente.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Use os seguintes elementos da API para alterar as taxas de reprodução:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, que especifica taxas válidas.

| **Valor da taxa** | **Efeito na reprodução** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Alterna para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Alterna para o modo de retrocesso rápido |
| 1,0 | Alterna para o modo de reprodução normal (chamar `play` é o mesmo que definir a propriedade rate como 1.0) |
| 0,0 | Pausas (chamar `pause` é o mesmo que definir a propriedade rate como 0,0) |