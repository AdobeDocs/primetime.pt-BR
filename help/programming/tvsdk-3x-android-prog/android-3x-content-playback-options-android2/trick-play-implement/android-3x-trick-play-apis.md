---
description: O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço rápido e retrocesso.
seo-description: O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço rápido e retrocesso.
seo-title: Elementos da API de alteração de taxa
title: Elementos da API de alteração de taxa
uuid: c2bcd20c-0641-4d75-802c-08098786d572
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Elementos da API de alteração de taxa {#rate-change-api-elements}

O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço rápido e retrocesso.

<!--<a id="section_E5D37C71323947E2AED8B866D9835E31"></a>-->

Use os seguintes elementos de API para alterar as taxas de reprodução:

* `PlaybackRateEvent.getRate`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.isTrickPlaySupported`
* `MediaPlayerItem.getAvailablePlaybackRates`, que especifica taxas válidas.

| **Valor da taxa** | **Efeito na reprodução** |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Alterna para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Alterna para o modo de retrocesso rápido |
| 1.0 | Alterna para o modo de reprodução normal (chamar `play` é o mesmo que definir a propriedade rate como 1.0) |
| 0.0 | Pausas (a chamada `pause` é a mesma que definir a propriedade rate como 0,0) |