---
description: Existem algumas limitações e alguns problemas na forma como o modo de truque de reprodução se comporta.
title: Limitações e comportamento para truques
exl-id: 98558970-9e5e-4dc1-a327-63d9db1d4fed
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Limitações e comportamento para truques{#limitations-and-behavior-for-trick-play}

Existem algumas limitações e alguns problemas na forma como o modo de truque de reprodução se comporta.

<!--<a id="section_8B88E281A0FA4661B4C2C70A0ABED57C"></a>-->

Estas são as limitações do modo de truque:

* A lista de reprodução principal deve conter segmentos somente de quadros I. Somente os quadros principais do I-frame track são exibidos na tela.
* A faixa de áudio e as legendas ocultas estão desativadas.
* A lógica de taxa de bits adaptável (ABR) está desabilitada. O TVSDK seleciona uma taxa de bits entre a taxa mais baixa fornecida e 800 kbps e usa essa taxa durante toda a sessão de trick-play.
* Reproduzir e pausar estão ativados.
* A busca não é permitida. Para buscar, chame `pause` para sair do modo de jogo e chamar `seek`.

* Você pode ir do modo de truque de reprodução para qualquer taxa de reprodução permitida (reprodução ou pausa).
* Quando os anúncios são incorporados no fluxo:

   * Você pode ir para a reprodução de truques somente ao reproduzir o conteúdo principal. Um erro é despachado se você tentar alternar para uma reprodução de truque durante um ad break.
   * Depois de iniciar o modo de execução de truque, os ad breaks são ignorados e nenhum evento de anúncio é acionado.
   * A linha do tempo exposta pelo TVSDK ao aplicativo do reprodutor não é modificada mesmo se os ad breaks forem ignorados.
   * O valor de tempo atual salta para frente (no avanço rápido) ou para trás (no retrocesso rápido) com a duração do ad break ignorado. Esse comportamento de salto para o tempo atual permite que a duração do fluxo permaneça inalterada durante a reprodução de truque. Seu aplicativo reprodutor pode obter o valor de hora local para rastrear o tempo relativo somente ao conteúdo principal. Nenhum salto de tempo é executado nos valores retornados para o horário local ao ignorar um anúncio.
   * A variável `MediaPlayerEvent.AD_BREAK_SKIPPED` O evento é despachado imediatamente antes de um ad break ser ignorado. Seu reprodutor pode usar esse evento para implementar uma lógica personalizada relacionada aos ad breaks ignorados.
   * Sair da reprodução de truque invoca a mesma política de reprodução de anúncio de quando sair da busca.

      Portanto, assim como na busca, o comportamento depende da diferença entre a política de reprodução do aplicativo e a padrão. O padrão é que o último ad break ignorado é reproduzido no ponto em que você sai do modo de reprodução inesperada.
