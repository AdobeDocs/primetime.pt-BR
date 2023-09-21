---
description: Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.
title: Implementar avanço e retrocesso rápidos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Implementar avanço e retrocesso rápidos{#implement-fast-forward-and-rewind}

Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.

>[!IMPORTANT]
>
>* O modo de reprodução de truques é compatível apenas com conteúdo MPEG Dash e HLS VOD.
>* O modo de reprodução de truques não é compatível com transmissões ou anúncios ao vivo.
>* Ao alternar do conteúdo principal para um anúncio, o TVSDK do navegador deixa o modo de reprodução artificial.
>

Para alternar a velocidade, você deve definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de truque de reprodução, definindo a taxa no `MediaPlayer` para um valor permitido.

   * A variável `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK do navegador seleciona a taxa permitida mais próxima se a taxa especificada não for permitida.

     A seguinte função de exemplo define a taxa:

     ```js
     setTrickPlayRate = function (player, trickPlayRate) { 
                   player.rate = trickPlayRate; 
     }
     ```

     A seguinte função de exemplo pode ser usada para consultar as taxas de reprodução disponíveis:

     ```js
     getAvailableTrickPlayRates = function (player) { 
              var item = player.currentItem; 
              var availableRates = item. availablePlaybackRates; 
              return availableRates; 
     } 
     ```

1. Opcionalmente, você pode acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente ocorre.

       O TVSDK do navegador despacha os seguintes eventos relacionados à reprodução:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando a variável `rate` O valor de é alterado para um valor diferente.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando a reprodução continua na taxa selecionada.

     O TVSDK do navegador despacha ambos os eventos quando o reprodutor retorna do modo de truque para o modo de reprodução normal.

## Elementos da API de alteração de taxa {#rate-change-API-elements}

O TVSDK do navegador inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se o trick play é compatível e outras funcionalidades relacionadas ao avanço e retrocesso rápidos.

Use os seguintes elementos de API para alterar as taxas de reprodução:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - especifica taxas válidas.

  | Valor da taxa | Efeito na reprodução |
  |---|---|
  | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Muda para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
  | -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 | Alterna para o modo de retrocesso rápido |
  | 1.0 | Muda para o modo normal de reprodução (chamando `play` é o mesmo que definir a propriedade rate como 1,0) |
  | 0.0 | Pausas (chamando `pause` é o mesmo que definir a propriedade rate como 0,0) |

## Limitações e comportamento para truques {#limitations-and-behavior-trick-play}

Existem algumas limitações e alguns problemas na forma como o modo de truque de reprodução se comporta.

Esta é uma lista das limitações do modo trick-play:

* Se o fluxo não contiver uma adaptação de jogo de truque, o rebobinamento rápido é desativado e a taxa máxima de reprodução para o avanço rápido é limitada a 8.
* Quando as adaptações de truque de reprodução são usadas para fornecer o modo de truque, a faixa de áudio é desativada.
* No modo de execução de truque, a alternância de faixas de áudio e legendas ocultas está desativada.
* Reproduzir e pausar estão ativados.
* Na busca, se a reprodução estiver no modo de truque, a taxa de reprodução será definida como 1 e a reprodução normal será retomada.
* A lógica da taxa de bits adaptável (ABR) está ativada.

  Ao usar as adaptações normais, os perfis são restritos entre `ABRControlParameters.minBitRate` e `ABRControlParameters.maxBitRate`. Ao usar adaptações de truques, os perfis são restritos entre `ABRControlParameters.minTrickPlayBitRate` e `ABRControlParameters.maxTrickPlayBitRate`.
