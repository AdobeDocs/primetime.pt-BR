---
description: Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.
title: Implementar avanço e retrocesso rápidos
exl-id: c1d70d46-449b-494b-9b89-5553e9bcdbc3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '775'
ht-degree: 0%

---

# Implementar avanço e retrocesso rápidos {#implement-fast-forward-and-rewind}

Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.

Para alternar a velocidade, você deve definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de truque de reprodução, configurando o `rate` propriedade no `MediaPlayer` para um valor permitido.

   * A variável `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK seleciona a taxa permitida mais próxima se a taxa especificada não for permitida.

      Quando a taxa de reprodução é alterada de 0 (pausa) ou 1 (reprodução normal) para uma taxa maior que 1 ou menor que -1, todos os anúncios na linha do tempo são removidos. Há apenas um período em toda a linha do tempo que facilita uma ação de reprodução para permitir que o conteúdo seja encaminhado e rebobinado rapidamente sem parar em qualquer posição de anúncio. Essa ação é ativada por uma ação de desanexação da linha do tempo no TVSDK para remover todos os adBreaks resolvidos. Quando a reprodução continua em 0 ou 1, os adBreaks são restaurados pela primeira ação de anexo da linha do tempo.

      Lembre-se das seguintes informações:

   * Se a ação de reprodução for retroceder o conteúdo, a reprodução continuará quando a taxa for alterada para 1.
   * Se a ação de reprodução for acelerar o conteúdo, o último adBreak ignorado será reproduzido na posição de retomada.

   Esse exemplo define a taxa de reprodução interna do reprodutor para a taxa solicitada.

   ```
   private function onPlaybackRateChange(event:IndexChangeEvent):void { 
       var newRateIndex:int = event.newIndex; 
       var newRate:Number = _playbackRates[newRateIndex]; 
   
       _player.rate = newRate; 
   } 
   ```

1. Opcionalmente, você pode acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente ocorre.

   O TVSDK despacha os seguintes eventos relacionados ao trick play:

   * `mediacore.events.PlaybackRateEvent.RATE_SELECTED` quando a variável `rate` O valor de é alterado para um valor diferente.

   * `mediacore.events.PlaybackRateEvent.RATE_PLAYING` quando a reprodução continua na taxa selecionada.

   O TVSDK despacha ambos os eventos quando o reprodutor retorna do modo &quot;trick-play&quot; para o modo de reprodução normal.

## Elementos da API de alteração de taxa {#rate-change-api}

O TVSDK inclui métodos, propriedades e eventos para determinar taxas válidas, taxas atuais, se o trick play é compatível e outras funcionalidades relacionadas ao avanço e retrocesso rápidos.

Use os seguintes elementos de API para alterar as taxas de reprodução:

* `MediaPlayer.rate` propriedade com funções setter e getter
* `MediaPlayer.localTime property` com a função getter
* `mediacore.events.PlaybackRateEvent.RATE_SELECTED`
* `mediacore.events.PlaybackRateEvent.RATE_PLAYING`
* `MediaPlayerItem.IsTrickPlaySupported` propriedade com a função getter
* `AdBreakPlaybackEvent.AD_BREAK_SKIPPED`
* `MediaPlayerItem.availablePlaybackRates` propriedade com função getter - especifica taxas válidas.

| Valor da taxa | Efeito na reprodução |
|---|---|
| 2.0, 4.0, 8.0, 16.0, 32.0, 64.0  , 128.0 | Muda para o modo de avanço rápido com o multiplicador especificado mais rápido que o normal (por exemplo, 4 é 4 vezes mais rápido que o normal) |
| -2.0, -4.0, -8.0, -16.0, -32.0, -64.0  , -128.0 | Alterna para o modo de retrocesso rápido |
| 1.0 | Muda para o modo normal de reprodução (chamando `play` é o mesmo que definir a propriedade rate como 1,0) |
| 0.0 | Pausas (chamando `pause` é o mesmo que definir a propriedade rate como 0,0) |

## Limitações e comportamento para truques {#limitations-behavior-trick-play}

Estas são as limitações do modo de truque:

* A lista de reprodução principal deve conter segmentos somente de quadros I. Somente os quadros principais do I-frame track são exibidos na tela.
* A faixa de áudio e as legendas ocultas estão desativadas.
* A lógica de taxa de bits adaptável (ABR) está desabilitada. O TVSDK seleciona uma taxa de bits entre a taxa mais baixa fornecida e 800 kbps e usa essa taxa durante toda a sessão de trick-play.
* Reproduzir e pausar estão ativados.
* A busca não é permitida. Para buscar, chame `pause` para sair do modo de jogo e chamar `seek`.

* Você pode sair do modo de truque de reprodução em qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando os anúncios são incorporados no fluxo:

   * Você pode ir para a reprodução de truques somente ao reproduzir o conteúdo principal. Um erro é despachado se você tentar alternar para uma reprodução de truque durante um ad break.
   * Depois de iniciar o modo de execução de truque, os ad breaks são ignorados e nenhum evento de anúncio é acionado.
   * A linha do tempo exposta pelo TVSDK ao aplicativo do reprodutor não é modificada mesmo se os ad breaks forem ignorados.
   * A variável `MediaPlayer.currentTime` a propriedade salta para frente (no avanço rápido) ou para trás (no retrocesso rápido) com a duração do ad break ignorado. Esse comportamento de salto para o tempo atual permite que a duração do fluxo permaneça inalterada durante a reprodução de truque. Seu aplicativo de reprodução pode usar o `localTime` propriedade para rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.

   * A variável `AdBreakPlaybackEvent.AD_BREAK_SKIPPED` O evento é despachado imediatamente antes de um ad break ser ignorado. Seu reprodutor pode usar esse evento para implementar uma lógica personalizada relacionada aos ad breaks ignorados.
   * Sair da reprodução de truque invoca a mesma política de reprodução de anúncio de quando sair da busca.

      Portanto, assim como na busca, o comportamento depende da diferença entre a política de reprodução do aplicativo e a padrão. O padrão é que o último ad break ignorado é reproduzido no ponto em que você sai da reprodução.
