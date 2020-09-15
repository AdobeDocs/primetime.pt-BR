---
description: A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera a reprodução para o start. Os recursos de Carregamento de anúncio com preguiça e Resolução de anúncios com preguiça podem reduzir esse atraso na inicialização.
keywords: Lazy;Ad resolving;Ad loading
seo-description: A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera a reprodução para o start. Os recursos de Carregamento de anúncio com preguiça e Resolução de anúncios com preguiça podem reduzir esse atraso na inicialização.
seo-title: Preguiçoso e resolução
title: Preguiçoso e resolução
uuid: cf9ba788-b83f-43aa-94c4-db391d92a77b
translation-type: tm+mt
source-git-commit: 5df9a8b98baaf1cd1803581d2b60c7ed4261a0e8
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Visão geral {#lazy-ad-resolving}

A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera a reprodução para o start. Os recursos de Carregamento de anúncio com preguiça e Resolução de anúncios com preguiça podem reduzir esse atraso na inicialização.

* Processo básico de resolução e carregamento de anúncios:

   1. O TVSDK baixa um manifesto (lista de reprodução) e *resolve* todos os anúncios.
   1. O TVSDK *carrega* todos os anúncios e os coloca na linha do tempo.
   1. O TVSDK move o player para o status PREPARADO e a reprodução do conteúdo é iniciada.

   O player usa os URLs no manifesto para obter o conteúdo do anúncio (criativos), garante que o conteúdo do anúncio esteja em um formato que o TVSDK possa reproduzir e o TVSDK coloca os anúncios na linha do tempo. Esse processo básico de resolver e carregar publicidades pode causar um atraso inaceitavelmente longo para um usuário que está aguardando para reproduzir seu conteúdo, especialmente se o manifesto contiver vários URLs de publicidade.

* *Carregamento* de anúncio com preguiça:

   1. O TVSDK baixa uma lista de reprodução e *resolve* todos os anúncios.
   1. O TVSDK *carrega* anúncios precedentes, move o player até o status PREPARADO e a reprodução do conteúdo é iniciada.
   1. O TVSDK *carrega* os anúncios restantes e os coloca na linha do tempo quando a reprodução ocorre.

   Esse recurso melhora o processo básico colocando o player no status PREPARADO antes que todos os anúncios sejam carregados.

* *Resolução* de anúncios ociosos:

   1. O TVSDK baixa a lista de reprodução.
   1. O TVSDK resolve e carrega qualquer anúncio precedente, move o player até o status PREPARADO e a reprodução do conteúdo é iniciada.
   1. O TVSDK resolve e carrega os anúncios restantes e os coloca na linha do tempo quando a reprodução ocorre.

   A resolução de anúncios ociosos baseia-se no carregamento de anúncios ociosos para permitir um start ainda mais rápido. Depois que o TVSDK coloca qualquer anúncio precedente, ele move o player para o status PREPARADO e, em seguida, resolve os anúncios adicionais e os coloca na linha do tempo.

>[!IMPORTANT]
>
>Fatores a serem considerados com a Resolução de anúncios ociosos:
>
>* A Resolução de anúncios ociosa está ativada por padrão. Se você desativá-la, todos os anúncios serão resolvidos antes dos start de reprodução.
>* A resolução de anúncios ociosos não permite busca ou trickplay até que todos os anúncios sejam resolvidos:

   >
   >    
   * O player deve aguardar o `kEventAdResolutionComplete` evento antes de permitir a busca ou a reprodução de truques.
   >    * Se o usuário tentar executar operações de busca ou de reprodução de artifício enquanto os anúncios ainda estiverem sendo resolvidos, o TVSDK emitirá o `kECLazyAdResolutionInProgress` erro.
   >    * Se necessário, o player deve atualizar a barra de depuração, *depois* de receber o `kEventAdResolutionComplete` evento.
>
>* A resolução de anúncios ociosos é apenas para VOD. Não funcionará com fluxos ao vivo.
>* A resolução de anúncios ociosos é incompatível com o recurso *Ativado* instantaneamente.

>
>  

Para obter mais informações sobre o Instant On, consulte instant-on .
>
>* Embora a resolução de anúncios ociosos resulte em uma reprodução muito mais rápida, se uma pausa de anúncio ocorrer nos primeiros 60 segundos de reprodução, ela pode não ser resolvida.
>* A resolução lenta do anúncio não afeta os anúncios precedentes.