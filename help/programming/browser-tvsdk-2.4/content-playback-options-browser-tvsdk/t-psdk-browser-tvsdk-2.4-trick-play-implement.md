---
description: Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.
seo-description: Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.
seo-title: Implementar para frente e retroceder rapidamente
title: Implementar para frente e retroceder rapidamente
uuid: c1992757-d067-4c11-8d08-fec09099476f
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '528'
ht-degree: 0%

---


# Implemente rapidamente para frente e recue{#implement-fast-forward-and-rewind}

Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.

>[!IMPORTANT]
>
>* O modo de reprodução de truques é compatível somente com conteúdo MPEG Dash e HLS VOD.
>* O modo de reprodução de truques não é compatível com streams ou anúncios ao vivo.
>* Ao alternar do conteúdo principal para um anúncio, o TVSDK do navegador deixa o modo de reprodução de truques.

>



Para mudar a velocidade, é necessário definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de reprodução de truque definindo a taxa em `MediaPlayer` para um valor permitido.

   * A classe `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK do navegador seleciona a taxa mais próxima permitida se a taxa especificada não for permitida.

      A função de exemplo a seguir define a taxa:

      ```js
      setTrickPlayRate = function (player, trickPlayRate) { 
                    player.rate = trickPlayRate; 
      }
      ```

      A seguinte função de exemplo pode ser usada para query das taxas de reprodução disponíveis:

      ```js
      getAvailableTrickPlayRates = function (player) { 
               var item = player.currentItem; 
               var availableRates = item. availablePlaybackRates; 
               return availableRates; 
      } 
      ```

1. Opcionalmente, você pode acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente acontece.

       O TVSDK do navegador despacha os seguintes eventos relacionados à reprodução de truques:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando o  `rate` valor muda para um valor diferente.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando a reprodução é retomada na taxa selecionada.

      O TVSDK do navegador despacha ambos os eventos quando o player retorna do modo de reprodução de truque para o modo de reprodução normal.

## Elementos de API de alteração de taxa {#rate-change-API-elements}

O TVSDK do navegador inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço e retrocesso rápidos.

Use os seguintes elementos de API para alterar as taxas de reprodução:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - especifica taxas válidas.

   | Valor da taxa | Efeito na reprodução |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Alterna para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
   | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | Alterna para o modo de retrocesso rápido |
   | 1,0 | Alterna para o modo de reprodução normal (chamar `play` é o mesmo que definir a propriedade rate como 1.0) |
   | 0,0 | Pausas (chamar `pause` é o mesmo que definir a propriedade rate como 0.0) |

## Limitações e comportamento para a reprodução de truques {#limitations-and-behavior-trick-play}

Há algumas limitações e alguns problemas na maneira como o modo de jogo de truque se comporta.

Esta é uma lista das limitações do modo de reprodução de truques:

* Se o fluxo não contiver uma adaptação para a reprodução de truques, o rebobinamento rápido será desativado e a taxa máxima de reprodução para avançar rapidamente será limitada a 8.
* Quando as adaptações de play de truque são usadas para fornecer o modo de truque, a faixa de áudio é desativada.
* No modo trick play, a alternância de faixas de áudio e legendas fechadas está desativada.
* Reproduzir e pausar são ativados.
* Em busca, se a reprodução estiver no modo de reprodução de truque, a taxa de reprodução será definida como 1 e a reprodução normal será retomada.
* A lógica da taxa de bits adaptável (ABR) está ativada.

   Ao usar adaptações normais, os perfis são restritos entre `ABRControlParameters.minBitRate` e `ABRControlParameters.maxBitRate`. Ao usar as adaptações de truque, os perfis são restritos entre `ABRControlParameters.minTrickPlayBitRate` e `ABRControlParameters.maxTrickPlayBitRate`.