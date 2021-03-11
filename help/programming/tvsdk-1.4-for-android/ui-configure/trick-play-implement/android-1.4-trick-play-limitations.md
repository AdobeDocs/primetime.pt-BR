---
description: Existem algumas limitações e alguns problemas na maneira como o modo de reprodução de truques se comporta.
title: Limitações e comportamento para a reprodução de truques
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Limitações e comportamento para a reprodução de truques{#limitations-and-behavior-for-trick-play}

Existem algumas limitações e alguns problemas na maneira como o modo de reprodução de truques se comporta.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Estas são as limitações do modo de reprodução de truque:

* A lista de reprodução principal deve conter segmentos somente I-frame. Apenas os quadros-chave da faixa de I-frame são exibidos na tela.
* A faixa de áudio e as legendas ocultas estão desativadas.
* A lógica da taxa de bits adaptativa (ABR) está desativada. O TVSDK seleciona uma taxa de bits entre a menor taxa fornecida e 800 kbps e usa essa taxa durante toda a sessão de trick-play.
* Reproduzir e pausar são ativados.
* Busca não é permitida. Para procurar, chame `pause` para sair do modo de reprodução de truque e chame `seek`.

* Você pode ir do modo de reprodução de truques para qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando anúncios são incorporados ao fluxo:

   * Você só pode usar o trick play ao reproduzir o conteúdo principal. Um erro é despachado se você tentar alternar para enganar a reprodução durante um ad break.
   * Depois de iniciar o modo de reprodução de truque, os ad breaks são ignorados e nenhum evento de anúncio é acionado.
   * A linha do tempo exposta pelo TVSDK ao aplicativo do reprodutor não é modificada mesmo que as quebras de anúncio sejam ignoradas.
   * O valor de tempo atual salta para a frente (em um avanço rápido) ou para trás (em um retrocesso rápido) com a duração do ad break ignorado. Esse comportamento de jump no tempo atual permite que a duração do fluxo permaneça não modificada durante a reprodução do truque. O aplicativo do reprodutor pode obter o valor de hora local para rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.
   * O evento `MediaPlayerEvent.AD_BREAK_SKIPPED` é despachado imediatamente antes que um ad break esteja prestes a ser ignorado. O reprodutor pode usar esse evento para implementar a lógica personalizada relacionada aos ad breaks ignorados.
   * Ao sair da busca, o recurso de trick play chama a mesma política de reprodução de anúncio.

      Portanto, como na busca, o comportamento depende da política de reprodução do aplicativo ser diferente do padrão. O padrão é que o último ad break ignorado é reproduzido no ponto em que você sai do modo de trick play.

