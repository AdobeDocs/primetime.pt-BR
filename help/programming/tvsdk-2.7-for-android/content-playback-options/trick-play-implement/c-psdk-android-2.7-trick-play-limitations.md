---
title: Limitações e comportamento para truques
description: Limitações e comportamento para truques
copied-description: true
exl-id: 5d9cae7b-d850-4ebc-8780-5abec847bb82
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---

# Limitações e comportamento para truques {#limitations-and-behavior-for-trick-play}

<!--<a id="section_2BC43539C5C142E085D06A7E35C76726"></a>-->

Limitações do modo de truque:

* A lista de reprodução principal deve conter segmentos somente Iframe.

   Somente os quadros principais do rastreamento de Iframe são exibidos na tela.
* A faixa de áudio e as legendas ocultas estão desativadas.
* Reproduzir e pausar estão ativados.
* Você pode sair do modo de truque de reprodução em qualquer taxa de reprodução permitida (reproduzir ou pausar).
* Quando os anúncios são incorporados no fluxo:

   * Você pode ir para a reprodução de truques somente ao reproduzir o conteúdo principal. Um erro é despachado se você tentar alternar para uma reprodução de truque durante um ad break.
   * Depois de iniciar o modo de reprodução de truque, os ad breaks são ignorados e nenhum evento de anúncio é acionado.
   * A linha do tempo exposta pelo TVSDK ao reprodutor não é modificada mesmo se os ad breaks forem ignorados.
   * O valor de tempo atual salta para frente (no avanço rápido) ou para trás (no retrocesso rápido) com a duração do ad break ignorado.

      Esse comportamento de salto para o tempo atual permite que a duração do fluxo permaneça inalterada durante a reprodução de truque. Seu reprodutor pode rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.
   * A variável `MediaPlayerEvent.AD_BREAK_SKIPPED` O evento é despachado imediatamente antes de um ad break ser ignorado.

      Seu reprodutor pode usar esse evento para implementar uma lógica personalizada relacionada aos ad breaks ignorados.

   * Sair da reprodução de truque invoca a mesma política de reprodução de anúncio de quando sair da busca.

      Assim como na busca, o comportamento depende da diferença entre a política de reprodução do aplicativo e a padrão. O padrão é que o último ad break ignorado é reproduzido no ponto em que você sai da reprodução.
