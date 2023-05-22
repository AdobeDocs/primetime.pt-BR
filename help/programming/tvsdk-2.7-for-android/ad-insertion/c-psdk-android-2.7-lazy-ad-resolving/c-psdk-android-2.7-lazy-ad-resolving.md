---
description: A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário aguardar o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncio lento podem reduzir esse atraso de inicialização.
keywords: Lento;Resolução de anúncios;Carregamento de anúncios
title: Resolução de anúncio lento
exl-id: 6f4c2b9b-a129-4132-8c88-259602222381
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Visão geral {#lazy-ad-resolving}

A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário aguardar o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncio lento podem reduzir esse atraso de inicialização.

* Processo básico de resolução e carregamento de anúncios:

   1. O TVSDK baixa um manifesto (lista de reprodução) e *resolve* todos os anúncios.
   1. TVSDK *cargas* todos os anúncios e os coloca na linha do tempo.
   1. O TVSDK move o reprodutor para o status PREPARADO e a reprodução do conteúdo começa.

   O reprodutor usa os URLs no manifesto para obter o conteúdo do anúncio (criações), garante que o conteúdo do anúncio esteja em um formato que o TVSDK possa reproduzir e o TVSDK coloca os anúncios na linha do tempo. Esse processo básico de resolução e carregamento de anúncios pode causar um atraso inaceitavelmente longo para um usuário que está aguardando para reproduzir seu conteúdo, especialmente se o manifesto contiver vários URLs de anúncios.

* *Carregamento lento de anúncio*:

   1. O TVSDK baixa uma lista de reprodução e *resolve* todos os anúncios.
   1. TVSDK *cargas* anúncios precedentes, move o reprodutor para o status PREPARADO e a reprodução do conteúdo é iniciada.
   1. TVSDK *cargas* os anúncios restantes e os coloca na linha do tempo conforme a reprodução ocorre.

   Esse recurso melhora o processo básico, colocando o reprodutor no status PREPARADO antes que todos os anúncios sejam carregados.

* *Resolução de anúncio lento*:

   1. O TVSDK baixa a lista de reprodução.
   1. O TVSDK resolve e carrega qualquer anúncio precedente, move o reprodutor para o status PREPARADO e a reprodução do conteúdo começa.
   1. O TVSDK resolve e carrega os anúncios restantes e os coloca na linha do tempo conforme a reprodução ocorre.

   A Resolução de anúncios lentos se baseia no Carregamento de anúncios lentos para permitir uma inicialização ainda mais rápida. Depois que o TVSDK coloca qualquer anúncio precedente, ele move o reprodutor para o status PREPARADO e, em seguida, resolve anúncios adicionais e os coloca na linha do tempo.

>[!IMPORTANT]
>
>Fatores a serem considerados na resolução de anúncios lentos:
>
>* A Resolução de anúncios lenta é ativada por padrão. Se você desativá-la, todos os anúncios serão resolvidos antes do início da reprodução.
>* A Resolução lenta de anúncios não permite a busca ou a reprodução de truques até que todos os anúncios sejam resolvidos:
   >
   >    * O reprodutor deve aguardar o `kEventAdResolutionComplete` antes de permitir a busca ou o jogo de truque.
   >    * Se o usuário tentar executar operações de busca ou reprodução enquanto os anúncios ainda estiverem sendo resolvidos, o TVSDK acionará a variável `kECLazyAdResolutionInProgress` erro.
   >    * Se necessário, o reprodutor deve atualizar a barra de limpeza, *após* recebendo o `kEventAdResolutionComplete` evento.
>
>* A resolução de anúncios ociosos é somente para VOD. Ele não funcionará com transmissões AO VIVO.
>* A Resolução de anúncios ociosos é incompatível com o *Instantâneo* recurso.
>
>  Para obter mais informações sobre a Ativação instantânea, consulte Ativação instantânea.
>
>* Embora a Resolução lenta do anúncio resulte em uma reprodução muito mais rápida, se um ad break ocorrer nos primeiros 60 segundos de reprodução, talvez não seja resolvido.
>* A resolução de anúncios lentos não afeta os anúncios precedentes.

