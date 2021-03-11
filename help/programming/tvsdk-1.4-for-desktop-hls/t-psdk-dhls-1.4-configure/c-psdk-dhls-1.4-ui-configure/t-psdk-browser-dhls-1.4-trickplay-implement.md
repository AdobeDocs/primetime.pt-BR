---
description: Quando os usuários avançam ou recuam rapidamente pela mídia, eles estão no modo de peça. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer com um valor diferente de 1.
title: Implementar rapidamente para a frente e retroceder
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---


# Implementar rapidamente para a frente e retroceder {#implement-fast-forward-and-rewind}

Quando os usuários avançam ou recuam rapidamente pela mídia, eles estão no modo de peça. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer com um valor diferente de 1.

Para alternar a velocidade, é necessário definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de reprodução por engano, definindo a propriedade `rate` no `MediaPlayer` para um valor permitido.

   * A classe `MediaPlayerItem` define as taxas de reprodução permitidas.
   * TVSDK seleciona a taxa mais próxima permitida se a taxa especificada não for permitida.

      Quando a taxa de trickplay é alterada de 0 (pausa) ou 1 (reprodução normal) para uma taxa maior que 1 ou menor que -1, todos os anúncios na linha do tempo são removidos. Há apenas um ponto na linha do tempo inteira que facilita uma ação de trickplay para permitir que o conteúdo seja encaminhado e revertido rapidamente sem parar em qualquer posição de anúncio. Essa ação é ativada por uma ação de desanexação da linha do tempo no TVSDK para remover todos os adBreaks resolvidos. Quando a trickplay é retomada em 0 ou 1, o adBreaks é restaurado pela primeira vez pela ação de anexo da linha do tempo.

      Lembre-se das seguintes informações:

   * Se a ação de trickplay for retroceder o conteúdo, a reprodução será retomada quando a taxa for alterada para 1.
   * Se a ação de trickplay tiver o objetivo de avançar rapidamente o conteúdo, o último adBreak ignorado será reproduzido na posição de retomada.

   Este exemplo define a taxa de reprodução interna do reprodutor para a taxa solicitada.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Opcionalmente, é possível acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente ocorre.

   O TVSDK despacha os seguintes eventos relacionados à reprodução de truque:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` quando o  `rate` valor muda para um valor diferente.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` quando a reprodução é retomada na taxa selecionada.

   O TVSDK despacha ambos os eventos quando o reprodutor volta do modo de trick-play para o modo de reprodução normal.

## Alterar taxa de elementos da API {#rate-change-api}

O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avançar e retroceder rapidamente.

Use os seguintes elementos da API para alterar as taxas de reprodução:

* `MediaPlayer.rate` propriedade com funções setter e getter
* `MediaPlayer.localTime property` com função getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` propriedade com função getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` propriedade com função getter - especifica taxas válidas.

| Valor da taxa | Efeito na reprodução |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0 , 128.0 | Alterna para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0 , -128.0 | Alterna para o modo de retrocesso rápido |
| 1,0 | Alterna para o modo de reprodução normal (chamar `play` é o mesmo que definir a propriedade rate como 1.0) |
| 0,0 | Pausas (chamar `pause` é o mesmo que definir a propriedade rate como 0,0) |

## Limitações e comportamento da reprodução de truques {#limitations-behavior-trick-play}

Estas são as limitações do modo de reprodução de truque:

* A lista de reprodução principal deve conter segmentos somente I-frame. Apenas os quadros-chave da faixa de I-frame são exibidos na tela.
* A faixa de áudio e as legendas ocultas estão desativadas.
* A lógica da taxa de bits adaptativa (ABR) está desativada. O TVSDK seleciona uma taxa de bits entre a menor taxa fornecida e 800 kbps e usa essa taxa durante toda a sessão de trick-play.
* Reproduzir e pausar são ativados.
* Busca não é permitida. Para procurar, chame `pause` para sair do modo de reprodução de truque e chame `seek`.

* Você pode sair do modo de reprodução de artifício em qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando anúncios são incorporados ao fluxo:

   * Você só pode usar o trick play ao reproduzir o conteúdo principal. Um erro é despachado se você tentar alternar para enganar a reprodução durante um ad break.
   * Depois de iniciar o modo de reprodução de truque, os ad breaks são ignorados e nenhum evento de anúncio é acionado.
   * A linha do tempo exposta pelo TVSDK ao aplicativo do reprodutor não é modificada mesmo que as quebras de anúncio sejam ignoradas.
   * A propriedade `MediaPlayer.currentTime` salta para a frente (em um avanço rápido) ou para trás (em rebentamento rápido) com a duração do ad break ignorado. Esse comportamento de jump no tempo atual permite que a duração do fluxo permaneça não modificada durante a reprodução do truque. O aplicativo do player pode usar a propriedade `localTime` para rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.

   * O evento `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` é despachado imediatamente antes que um ad break esteja prestes a ser ignorado. O reprodutor pode usar esse evento para implementar a lógica personalizada relacionada aos ad breaks ignorados.
   * Ao sair da busca, o recurso de trick play chama a mesma política de reprodução de anúncio.

      Portanto, como na busca, o comportamento depende da política de reprodução do aplicativo ser diferente do padrão. O padrão é que o último ad break ignorado é reproduzido no ponto em que você sai do trick play.