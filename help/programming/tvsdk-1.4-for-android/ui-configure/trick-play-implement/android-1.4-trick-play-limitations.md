---
description: Há algumas limitações e alguns problemas na maneira como o modo de jogo de truque se comporta.
seo-description: Há algumas limitações e alguns problemas na maneira como o modo de jogo de truque se comporta.
seo-title: Limitações e comportamento para a reprodução de truques
title: Limitações e comportamento para a reprodução de truques
uuid: 0e84c9ef-fc18-4667-ad17-7f4777b552ba
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Limitações e comportamento para a reprodução de truques{#limitations-and-behavior-for-trick-play}

Há algumas limitações e alguns problemas na maneira como o modo de jogo de truque se comporta.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Estas são as limitações para o modo de reprodução de truques:

* A lista de reprodução mestre deve conter segmentos somente I-frame. Somente os quadros principais da faixa de I-frame são exibidos na tela.
* A faixa de áudio e as legendas fechadas estão desativadas.
* A lógica da taxa de bits adaptável (ABR) está desativada. O TVSDK seleciona uma taxa de um bit entre a taxa mais baixa fornecida e 800 kbps e usa essa taxa durante toda a sessão de jogo de artifício.
* Reproduzir e pausar são ativados.
* Busca não é permitida. Para buscar, chame `pause` para sair do modo de jogo de truque e chame `seek`.

* Você pode ir do modo de reprodução de truque para qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando os anúncios forem incorporados no fluxo:

   * Você só pode usar o recurso de engano enquanto reproduz o conteúdo principal. Um erro é despachado se você tentar alternar para a reprodução de truques durante uma pausa de anúncio.
   * Depois de iniciar o modo de reprodução de truque, as pausas de anúncio são ignoradas e nenhum evento de anúncio é acionado.
   * A linha do tempo exposta pelo TVSDK ao aplicativo do player não é modificada mesmo se as quebras de anúncio forem ignoradas.
   * O valor atual salta para frente (para frente) ou para trás (com rebobinamento rápido) com a duração do intervalo de anúncios ignorado. Esse comportamento de salto para o tempo atual permite que a duração do fluxo permaneça não modificada durante a reprodução do truque. O aplicativo do player pode obter o valor de hora local para rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.
   * O `MediaPlayerEvent.AD_BREAK_SKIPPED` evento é despachado imediatamente antes que um intervalo de anúncios esteja prestes a ser ignorado. Seu player pode usar esse evento para implementar a lógica personalizada relacionada às pausas de anúncio ignoradas.
   * Sair da reprodução de truques invoca a mesma política de reprodução de anúncios que ao sair da busca.

      Portanto, como na busca, o comportamento depende se a política de reprodução do aplicativo é diferente do padrão. O padrão é que o último intervalo de anúncios ignorado é reproduzido no ponto em que você sai do modo de reprodução de truques.

