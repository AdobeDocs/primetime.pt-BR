---
description: Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.
seo-description: Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.
seo-title: Implementar para frente e retroceder rapidamente
title: Implementar para frente e retroceder rapidamente
uuid: bd190534-c871-4673-b79d-1413277f480f
translation-type: tm+mt
source-git-commit: 5a786d8001326f874a51d65b8e8badca44f46e96
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---


# Implemente rapidamente para frente e recue {#implement-fast-forward-and-rewind}

Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.

Para mudar a velocidade, é necessário definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de reprodução de truque definindo a propriedade `rate` em `MediaPlayer` para um valor permitido.

   * A classe `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK seleciona a taxa mais próxima permitida se a taxa especificada não for permitida.

      Quando a taxa de trickplay é alterada de 0 (pausa) ou 1 (reprodução normal) para uma taxa maior que 1 ou menor que -1, todos os anúncios na linha do tempo são removidos. Há apenas um período em toda a linha do tempo que facilita uma ação de trickplay para permitir que o conteúdo seja rapidamente encaminhado e revertido sem parar em qualquer posição de anúncio. Esta ação é ativada por uma ação de desanexação da linha do tempo no TVSDK para remover todos os adBreaks resolvidos. Quando o trickplay é retomado em 0 ou 1, o adBreaks é restaurado pela ação de anexo da linha do tempo.

      Lembre-se das seguintes informações:

   * Se a ação de trickplay for rebobinar o conteúdo, a reprodução será retomada quando a taxa for alterada para 1.
   * Se a ação de trickplay for avançar rapidamente o conteúdo, o último adBreak ignorado será reproduzido na posição de retomada.

   Este exemplo define a taxa de reprodução interna do player para a taxa solicitada.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Opcionalmente, você pode acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente acontece.

   O TVSDK despacha os seguintes eventos relacionados à reprodução de truques:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` quando o  `rate` valor muda para um valor diferente.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` quando a reprodução é retomada na taxa selecionada.

   O TVSDK despacha ambos os eventos quando o player retorna do modo de reprodução de truque para o modo de reprodução normal.

## Elementos de API de alteração de taxa {#rate-change-api}

O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se a reprodução de truques é suportada e outras funcionalidades relacionadas a avanço e retrocesso rápidos.

Use os seguintes elementos de API para alterar as taxas de reprodução:

* `MediaPlayer.rate` propriedade com funções setter e getter
* `MediaPlayer.localTime property` com função getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` propriedade com função getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` propriedade com função getter - especifica taxas válidas.

| Valor da taxa | Efeito na reprodução |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0, 128.0 | Alterna para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0, -128.0 | Alterna para o modo de retrocesso rápido |
| 1,0 | Alterna para o modo de reprodução normal (chamar `play` é o mesmo que definir a propriedade rate como 1.0) |
| 0,0 | Pausas (chamar `pause` é o mesmo que definir a propriedade rate como 0.0) |

## Limitações e comportamento para a reprodução de truques {#limitations-behavior-trick-play}

Estas são as limitações para o modo de reprodução de truques:

* A lista de reprodução principal deve conter segmentos somente I-frame. Somente os quadros principais da faixa de I-frame são exibidos na tela.
* A faixa de áudio e as legendas fechadas estão desativadas.
* A lógica da taxa de bits adaptável (ABR) está desativada. O TVSDK seleciona uma taxa de um bit entre a taxa mais baixa fornecida e 800 kbps e usa essa taxa durante toda a sessão de jogo de artifício.
* Reproduzir e pausar são ativados.
* Busca não é permitida. Para buscar, chame `pause` para sair do modo de jogo de truque e chame `seek`.

* Você pode sair do modo de reprodução de truques em qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando os anúncios forem incorporados no fluxo:

   * Você só pode usar o recurso de engano enquanto reproduz o conteúdo principal. Um erro é despachado se você tentar alternar para a reprodução de truques durante uma pausa de anúncio.
   * Depois de iniciar o modo de reprodução de truque, as pausas de anúncio são ignoradas e nenhum evento de anúncio é disparado.
   * A linha do tempo exposta pelo TVSDK ao aplicativo do player não é modificada mesmo se as quebras de anúncio forem ignoradas.
   * A propriedade `MediaPlayer.currentTime` salta para frente (para frente) ou para trás (com rebobinamento rápido) com a duração do intervalo de anúncios ignorado. Esse comportamento de salto para o tempo atual permite que a duração do fluxo permaneça não modificada durante a reprodução do truque. O aplicativo do player pode usar a propriedade `localTime` para rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.

   * O evento `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` é despachado imediatamente antes que um intervalo de anúncios esteja prestes a ser ignorado. Seu player pode usar esse evento para implementar a lógica personalizada relacionada às pausas de anúncio ignoradas.
   * Sair da reprodução de truques invoca a mesma política de reprodução de anúncios que ao sair da busca.

      Portanto, como na busca, o comportamento depende se a política de reprodução do aplicativo é diferente do padrão. O padrão é que o último intervalo de anúncios ignorado é reproduzido no ponto em que você sai da peça.