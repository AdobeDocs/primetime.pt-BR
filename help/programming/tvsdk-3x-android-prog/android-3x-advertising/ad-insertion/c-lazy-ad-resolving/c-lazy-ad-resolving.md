---
description: A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário que aguarda o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncios lento podem reduzir esse atraso de inicialização. A resolução de anúncios ociosos mudou significativamente na versão 3.0. No carregamento de Anúncio lento anterior ao 3.0, a resolução do anúncio foi dividida em duas etapas, resolvendo apenas anúncios precedentes antes do status PREPARADO, e os cilindros médios e posteriores após o status PREPARADO. Isso foi alterado e os ad breaks agora são resolvidos em um intervalo especificado antes da posição do ad break.
keywords: Preguiçoso;Resolução de anúncio;Carregamento de anúncio
title: Solução de anúncios em tempo real
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---


# Visão geral {#just-in-time-ad-resolving-overview}

A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário que aguarda o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncios lento podem reduzir esse atraso de inicialização. A resolução de anúncios ociosos mudou significativamente na versão 3.0. No carregamento de Anúncio lento anterior ao 3.0, a resolução do anúncio foi dividida em duas etapas, resolvendo apenas anúncios precedentes antes do status PREPARADO, e os cilindros médios e posteriores após o status PREPARADO. Isso foi alterado e os ad breaks agora são resolvidos em um intervalo especificado antes da posição do ad break.

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
   1. O TVSDK resolve e cada um dos anúncios restantes é dividido individualmente com base no seguinte cálculo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      Por padrão, para conteúdo com 6 segundos de duração do Target, será de 5,0 + 30,0 + 6,0 segundos (41 segundos)

   1. Se um ad break ocorrer dentro de 10 segundos da posição inicial, ele será resolvido junto com anúncios precedentes antes do status PREPARED.

>[!IMPORTANT]
>
>**Fatores a serem considerados com a resolução de anúncios ociosos:**
>
>* A resolução de anúncios preguiçosa só é compatível com fluxos VOD somente com modos SERVER_MAP e MANIFEST_CUES.
>* A resolução de anúncios ociosos não está ativada por padrão. Se estiver desativado, todos os anúncios serão resolvidos em fluxos VOD antes do início da reprodução.
>* A resolução de anúncios ociosos é incompatível com o recurso Instant On . Para obter mais informações sobre o Instant On, consulte Instant On.
>* Com a resolução de anúncios preguiçosa, enquanto busca um avanço em um ad break, o ad break mais próximo para a posição da busca será resolvido durante a busca.
>* Com a resolução de anúncios lento, se houver várias quebras de anúncios ao mesmo tempo (VMAP), elas serão resolvidas ao mesmo tempo.
>* Não é recomendável reduzir o valor de *setDelayAdLoadingTolerance() *abaixo do valor padrão (5 segundos). Isso pode fazer com que o reprodutor &quot;armazene em buffer&quot; desnecessariamente.
>* A resolução de anúncios ociosos não afeta os anúncios precedentes.
>* Atualmente, a resolução de anúncios lento é compatível com o Plug-in Auditude. É recomendável não definir *setDelayAdLoading* como true se estiver usando um resolvedor personalizado.

>


