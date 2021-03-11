---
title: Limitações e comportamento para a reprodução de truques
description: Limitações e comportamento para a reprodução de truques
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Limitações e comportamento da reprodução de truques {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitações para o modo de reprodução de truques:

* A lista de reprodução principal deve conter segmentos somente Iframe.

   Somente os quadros principais do rastreamento de Iframe são exibidos na tela.
* A faixa de áudio e as legendas ocultas estão desativadas.
* Reproduzir e pausar são ativados.
* Você pode sair do modo de reprodução de artifício em qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando anúncios são incorporados ao fluxo:

   * Você só pode usar o trick play ao reproduzir o conteúdo principal. Um erro é despachado se você tentar alternar para enganar a reprodução durante um ad break.
   * Após iniciar o modo de reprodução de truque, os ad breaks são ignorados e nenhum evento de anúncio é acionado.
   * A linha do tempo exposta pelo TVSDK ao reprodutor não é modificada mesmo se as quebras de anúncios forem ignoradas.
   * O valor de tempo atual salta para a frente (em um avanço rápido) ou para trás (em um retrocesso rápido) com a duração do ad break ignorado.

      Esse comportamento de jump no tempo atual permite que a duração do fluxo permaneça não modificada durante a reprodução do truque. O reprodutor pode rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.
   * O evento `MediaPlayerEvent.AD_BREAK_SKIPPED` é despachado imediatamente antes que um ad break esteja prestes a ser ignorado.

      O reprodutor pode usar esse evento para implementar a lógica personalizada relacionada aos ad breaks ignorados.

   * Ao sair da busca, o recurso de trick play chama a mesma política de reprodução de anúncio.

      Assim como com a busca, o comportamento depende da política de reprodução do aplicativo ser diferente do padrão. O padrão é que o último ad break ignorado é reproduzido no ponto em que você sai do trick play.