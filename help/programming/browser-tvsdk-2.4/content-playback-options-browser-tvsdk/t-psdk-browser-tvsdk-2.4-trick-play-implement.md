---
description: Quando os usuários avançam ou recuam rapidamente pela mídia, eles estão no modo de peça. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer com um valor diferente de 1.
title: Implementar rapidamente para a frente e retroceder
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---


# Implementar rapidamente para a frente e retroceder{#implement-fast-forward-and-rewind}

Quando os usuários avançam ou recuam rapidamente pela mídia, eles estão no modo de peça. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer com um valor diferente de 1.

>[!IMPORTANT]
>
>* O modo Trick play é compatível somente com conteúdo MPEG Dash e VOD de HLS.
>* O modo Trick play não é compatível com fluxos ao vivo ou anúncios.
>* Ao alternar do conteúdo principal para um anúncio, o TVSDK do navegador deixa o modo de reprodução de truques.

>



Para alternar a velocidade, é necessário definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de reprodução por engano, definindo a taxa no `MediaPlayer` para um valor permitido.

   * A classe `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK do navegador seleciona a taxa mais próxima permitida se a taxa especificada não for permitida.

      A função de exemplo a seguir define a taxa:

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

1. Opcionalmente, é possível acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente ocorre.

       O TVSDK do navegador despacha os seguintes eventos relacionados à reprodução de truque:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando o  `rate` valor muda para um valor diferente.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando a reprodução é retomada na taxa selecionada.

      O TVSDK do navegador despacha ambos os eventos quando o reprodutor volta do modo de reprodução de truque para o modo de reprodução normal.

## Alterar taxa de elementos da API {#rate-change-API-elements}

O TVSDK do navegador inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avançar e retroceder rapidamente.

Use os seguintes elementos da API para alterar as taxas de reprodução:

* `MediaPlayer.rate`
* `PlaybackRateEvent.rate`
* `MediaPlayerItem.istrickPlaySupported`
* `MediaPlayerItem.availablePlaybackRates` - especifica taxas válidas.

   | Valor da taxa | Efeito na reprodução |
   |---|---|
   | 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 | Alterna para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
   | -2,0, -4,0, -8,0, -16,0, -32,0, -64,0 | Alterna para o modo de retrocesso rápido |
   | 1,0 | Alterna para o modo de reprodução normal (chamar `play` é o mesmo que definir a propriedade rate como 1.0) |
   | 0,0 | Pausas (chamar `pause` é o mesmo que definir a propriedade rate como 0,0) |

## Limitações e comportamento da reprodução de truques {#limitations-and-behavior-trick-play}

Existem algumas limitações e alguns problemas na maneira como o modo de reprodução de truques se comporta.

Veja a seguir uma lista das limitações do modo de reprodução:

* Se o fluxo não contiver uma adaptação de reprodução de truque, o retrocesso rápido será desativado e a taxa máxima de reprodução para avançar rapidamente será limitada a 8.
* Quando as adaptações de trick play são usadas para fornecer o modo de trick , a faixa de áudio é desativada.
* No modo de reprodução de artifício, a alternância das faixas de áudio e legendas ocultas está desativada.
* Reproduzir e pausar são ativados.
* Na busca, se a reprodução estiver no modo de reprodução de truque, a taxa de reprodução será definida como 1 e a reprodução normal será retomada.
* A lógica da taxa de bits adaptável (ABR) está ativada.

   Ao usar adaptações normais, os perfis são restritos entre `ABRControlParameters.minBitRate` e `ABRControlParameters.maxBitRate`. Ao usar adaptações de truques, os perfis são restritos entre `ABRControlParameters.minTrickPlayBitRate` e `ABRControlParameters.maxTrickPlayBitRate`.