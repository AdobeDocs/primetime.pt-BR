---
description: O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço e retrocesso rápidos.
seo-description: O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço e retrocesso rápidos.
seo-title: Elementos da API de alteração de taxa
title: Elementos da API de alteração de taxa
uuid: 0040d35c-f9cb-4066-9bee-828ed5541194
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Elementos da API de alteração de taxa{#rate-change-api-elements}

O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço e retrocesso rápidos.

<!--<a id="section_36576E92DE6343AEBD0BBD662502365D"></a>-->

Use os seguintes elementos de API para alterar as taxas de reprodução:

* `PlaybackRateEvent.getRate`
* `MediaPlayer.getLocalTime`
* `MediaPlayerEvent.RATE_SELECTED`
* `MediaPlayerEvent.RATE_PLAYING`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.getAvailablePlaybackRates` - especifica taxas válidas.

| Valor da taxa | Efeito na reprodução |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Alterna para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Alterna para o modo de retrocesso rápido |
| 1.0 | Alterna para o modo de reprodução normal (chamar `play` é o mesmo que definir a propriedade rate como 1.0) |
| 0.0 | Pausas (a chamada `pause` é a mesma que definir a propriedade rate como 0,0) |

