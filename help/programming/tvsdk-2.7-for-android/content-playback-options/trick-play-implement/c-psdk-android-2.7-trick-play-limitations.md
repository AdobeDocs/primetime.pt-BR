---
description: nulo
seo-description: nulo
seo-title: Limitações e comportamento para a reprodução de truques
title: Limitações e comportamento para a reprodução de truques
uuid: 5b947075-eba0-45de-82d0-50b193f1ac83
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---


# Limitações e comportamento para a reprodução de truques {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitações para o modo de jogo:

* A lista de reprodução principal deve conter segmentos somente Iframe.

   Somente os quadros principais do rastreamento Iframe são exibidos na tela.
* A faixa de áudio e as legendas fechadas estão desativadas.
* Reproduzir e pausar são ativados.
* Você pode sair do modo de reprodução de truques em qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando os anúncios forem incorporados no fluxo:

   * Você só pode usar o recurso de engano enquanto reproduz o conteúdo principal. Um erro é despachado se você tentar alternar para a reprodução de truques durante uma pausa de anúncio.
   * Após iniciar o modo de reprodução de truque, as quebras de anúncio são ignoradas e nenhum evento de anúncio é disparado.
   * A linha do tempo exposta pelo TVSDK ao player não é modificada mesmo se as quebras de anúncio forem ignoradas.
   * O valor atual salta para frente (para frente) ou para trás (com rebobinamento rápido) com a duração do intervalo de anúncios ignorado.

      Esse comportamento de salto para o tempo atual permite que a duração do fluxo permaneça não modificada durante a reprodução do truque. Seu player pode rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.
   * O evento `MediaPlayerEvent.AD_BREAK_SKIPPED` é despachado imediatamente antes que um intervalo de anúncios esteja prestes a ser ignorado.

      Seu player pode usar esse evento para implementar a lógica personalizada relacionada às pausas de anúncio ignoradas.

   * Sair da reprodução de truques invoca a mesma política de reprodução de anúncios que ao sair da busca.

      Assim como com a busca, o comportamento depende de se a política de reprodução do aplicativo é diferente do padrão. O padrão é que o último intervalo de anúncios ignorado é reproduzido no ponto em que você sai da peça.

