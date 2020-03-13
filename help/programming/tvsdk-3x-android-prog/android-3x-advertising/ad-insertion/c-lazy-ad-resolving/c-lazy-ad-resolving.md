---
description: A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera o início da reprodução. Os recursos de Carregamento de anúncio com preguiça e Resolução de anúncios com preguiça podem reduzir esse atraso na inicialização. A resolução de anúncios ociosos mudou significativamente na versão 3.0. No carregamento de Anúncio com preguiça anterior à 3.0, a resolução do anúncio foi dividida em duas etapas, resolvendo apenas os anúncios anteriores ao status PREPARADO e mid-rolls e post-rolls após o status PREPARADO. Isso foi alterado e as quebras de anúncio agora são resolvidas em um intervalo especificado antes da posição do intervalo do anúncio.
keywords: Lazy;Ad resolving;Ad loading
seo-description: A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera o início da reprodução. Os recursos de Carregamento de anúncio com preguiça e Resolução de anúncios com preguiça podem reduzir esse atraso na inicialização. A resolução de anúncios ociosos mudou significativamente na versão 3.0. No carregamento de Anúncio com preguiça anterior à 3.0, a resolução do anúncio foi dividida em duas etapas, resolvendo apenas os anúncios anteriores ao status PREPARADO e mid-rolls e post-rolls após o status PREPARADO. Isso foi alterado e as quebras de anúncio agora são resolvidas em um intervalo especificado antes da posição do intervalo do anúncio.
seo-title: Resolução de anúncios just-in-time
title: Resolução de anúncios just-in-time
uuid: 77028f6e-7e53-45d1-bcc0-54f8224d6d18
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Visão geral {#just-in-time-ad-resolving-overview}

A resolução e o carregamento do anúncio podem causar um atraso inaceitável para um usuário que espera o início da reprodução. Os recursos de Carregamento de anúncio com preguiça e Resolução de anúncios com preguiça podem reduzir esse atraso na inicialização. A resolução de anúncios ociosos mudou significativamente na versão 3.0. No carregamento de Anúncio com preguiça anterior à 3.0, a resolução do anúncio foi dividida em duas etapas, resolvendo apenas os anúncios anteriores ao status PREPARADO e mid-rolls e post-rolls após o status PREPARADO. Isso foi alterado e as quebras de anúncio agora são resolvidas em um intervalo especificado antes da posição do intervalo do anúncio.

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
   1. O TVSDK resolve e cada uma das quebras de anúncio restantes individualmente com base no seguinte cálculo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      Por padrão, para conteúdo com uma duração de Target de 6 segundos, será de 5,0 + 30,0 + 6,0 segundos (41 segundos)

   1. Se ocorrer uma quebra de anúncio dentro de 10 segundos após a posição inicial, ela será resolvida junto com os anúncios precedentes antes do status PREPARADO.

>[!IMPORTANT]
>
>**Fatores a serem considerados com a Resolução de anúncios ociosos:** >
>* A resolução de anúncios lenta só é suportada para fluxos VOD somente com modos SERVER_MAP e MANIFEST_CUES.
>* Por padrão, a Resolução de anúncios ociosos não está ativada. Se estiver desativado, todos os anúncios serão resolvidos em fluxos VOD antes do início da reprodução.
>* A resolução de anúncios ociosos é incompatível com o recurso Ativado instantaneamente. Para obter mais informações sobre o Instant On (Ativado instantaneamente), consulte Instant On (Ativado instantaneamente).
>* Com a Resolução de anúncios ociosos, ao mesmo tempo em que procura um intervalo de um anúncio, o intervalo mais próximo à posição de busca será resolvido durante a busca.
>* Com a Resolução de anúncios ociosos, se houver várias interrupções de anúncios ao mesmo tempo (VMAP), elas serão resolvidas ao mesmo tempo.
>* Não é recomendável reduzir o valor de *setDelayAdLoadingTolerance() *abaixo do valor padrão (5 segundos). Isso pode fazer com que o player &quot;amorteca&quot; desnecessariamente.
>* A resolução de anúncios ociosos não afeta os anúncios precedentes.
>* Atualmente, a Resolução de anúncios ociosos é compatível com o Auditude-Plugin. É recomendável não definir ** setDelayAdLoadingcomo verdadeiro se você estiver usando um resolvedor personalizado.
>


