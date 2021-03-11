---
description: A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário que aguarda o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncios lento podem reduzir esse atraso de inicialização.
keywords: Preguiçoso;Resolução de anúncio;Carregamento de anúncio
title: Lento e solucionando
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---


# Visão geral {#lazy-ad-resolving}

A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário que aguarda o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncios lento podem reduzir esse atraso de inicialização.

* Processo básico de resolução e carregamento de anúncios:

   1. O TVSDK baixa um manifesto (lista de reprodução) e *resolve* todos os anúncios.
   1. O TVSDK *carrega* todos os anúncios e os coloca na linha do tempo.
   1. O TVSDK move o reprodutor para o status PREPARADO, e a reprodução do conteúdo é iniciada.

   O reprodutor usa os URLs no manifesto para obter o conteúdo do anúncio (criações), garante que o conteúdo do anúncio esteja em um formato que TVSDK possa reproduzir e TVSDK coloca os anúncios na linha do tempo. Esse processo básico de resolver e carregar anúncios pode causar um atraso inaceitavelmente longo para um usuário esperando para reproduzir seu conteúdo, especialmente se o manifesto contiver vários URLs de anúncio.

* *Carregamento* de anúncio lento:

   1. O TVSDK baixa uma lista de reprodução e *resolve* todos os anúncios.
   1. O TVSDK *carrega* anúncios precedentes, move o reprodutor para o status PREPARADO e a reprodução do conteúdo é iniciada.
   1. O TVSDK *carrega* os anúncios restantes e os coloca na linha do tempo quando a reprodução ocorre.

   Esse recurso melhora o processo básico ao colocar o reprodutor no status PREPARED antes que todos os anúncios sejam carregados.

* *Resolução* de anúncios ociosos:

   1. TVSDK baixa a lista de reprodução.
   1. O TVSDK resolve e carrega qualquer anúncio precedente, move o reprodutor para o status PREPARADO e a reprodução do conteúdo é iniciada.
   1. O TVSDK resolve e carrega os anúncios restantes e os coloca na linha do tempo quando a reprodução ocorre.

   A resolução de anúncios lento baseia-se no carregamento lento de anúncios para permitir uma inicialização ainda mais rápida. Depois que o TVSDK adiciona quaisquer anúncios precedentes, ele move o reprodutor para o status PREPARADO e, em seguida, resolve anúncios adicionais e os coloca na linha do tempo.

>[!IMPORTANT]
>
>Fatores a serem considerados com a resolução de anúncios ociosos:
>
>* A resolução de anúncios ociosos é ativada por padrão. Se você desativá-lo, todos os anúncios serão resolvidos antes do início da reprodução.
>* A resolução de anúncios preguiçosos não permite busca ou trickplay até que todos os anúncios sejam resolvidos:

   >
   >    
   * O reprodutor deve aguardar o evento `kEventAdResolutionComplete` antes de permitir a busca ou a reprodução do truque.
   >    * Se o usuário tentar executar operações de busca ou de reprodução de truque enquanto os anúncios ainda estão sendo resolvidos, o TVSDK acionará o erro `kECLazyAdResolutionInProgress`.
   >    * Se necessário, o reprodutor deve atualizar a barra de depuração, *depois de* receber o evento `kEventAdResolutionComplete`.
>
>* A resolução de anúncios lento é somente para VOD. Ele não funcionará com fluxos AO VIVO.
>* A resolução de anúncios preguiçosos é incompatível com o recurso *Ativado instantaneamente*.

>
>  

Para obter mais informações sobre o Instant On, consulte instantâneo .
>
>* Embora a resolução de anúncios lento resulte em uma reprodução muito mais rápida, se um ad break ocorrer nos primeiros 60 segundos de reprodução, ela pode não ser resolvida.
>* A resolução de anúncios ociosos não afeta anúncios precedentes.