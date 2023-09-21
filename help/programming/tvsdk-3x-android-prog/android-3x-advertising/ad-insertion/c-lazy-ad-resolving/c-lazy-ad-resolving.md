---
description: A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário aguardar o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncio lento podem reduzir esse atraso de inicialização. A Resolução de anúncios lentos foi alterada significativamente na versão 3.0. No carregamento lento de anúncios antes da versão 3.0, a resolução de anúncios foi dividida em duas etapas, resolvendo apenas anúncios precedentes ao status PREPARADO e anúncios intermediários e posteriores ao status PREPARADO. Isso mudou e os ad breaks agora são resolvidos em um intervalo especificado antes da posição do ad break.
keywords: Lento;Resolução de anúncios;Carregamento de anúncios
title: Resolução de anúncios just-in-time
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Visão geral {#just-in-time-ad-resolving-overview}

A resolução e o carregamento de anúncios podem causar um atraso inaceitável para um usuário aguardar o início da reprodução. Os recursos de Carregamento de anúncio lento e Resolução de anúncio lento podem reduzir esse atraso de inicialização. A Resolução de anúncios lentos foi alterada significativamente na versão 3.0. No carregamento lento de anúncios antes da versão 3.0, a resolução de anúncios foi dividida em duas etapas, resolvendo apenas anúncios precedentes ao status PREPARADO e anúncios intermediários e posteriores ao status PREPARADO. Isso mudou e os ad breaks agora são resolvidos em um intervalo especificado antes da posição do ad break.

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
   1. O TVSDK resolve e cada um dos ad breaks restantes individualmente com base no seguinte cálculo:

      `AdvertisingMetadata::getDelayAdLoadingTolerance() + PlayBufferTime::playBufferTime + the value defined in EXT-X-TARGETDURATION`

      Por padrão, para conteúdo com duração de 6 segundos do Target, será 5,0 + 30,0 + 6,0 segundos (41 segundos)

   1. Se um ad break ocorrer em até 10 segundos da posição inicial, ele será resolvido junto com os anúncios precedentes ao status PREPARADO.

>[!IMPORTANT]
>
>**Fatores a serem considerados na resolução de anúncios lentos:**
>
>* A Resolução de Anúncios Lentos só é suportada para fluxos de VOD com os modos SERVER_MAP e MANIFEST_CUES.
>* A Resolução de anúncios lenta não é ativada por padrão. Se desativado, todos os anúncios são resolvidos em fluxos de VOD antes do início da reprodução.
>* A Resolução de Anúncios Lentos é incompatível com o recurso de Ativação Instantânea. Para obter mais informações sobre Ativação instantânea, consulte Ativação instantânea.
>* Com a Resolução de anúncio lento, enquanto busca adiante por um ad break, o ad break mais próximo da posição de busca será resolvido durante a busca.
>* Com a Resolução de anúncios ociosos, se houver vários ad breaks ao mesmo tempo (VMAP), eles serão resolvidos ao mesmo tempo.
>* Não é recomendável reduzir o valor de *setDelayAdLoadingTolerance() *abaixo do valor padrão (5 segundos). Isso pode fazer com que o reprodutor &quot;armazene em buffer&quot; desnecessariamente.
>* A Resolução de anúncios lentos não afeta os anúncios precedentes.
>* Atualmente, a Resolução de anúncios lentos é suportada com o plug-in Auditude. É recomendável não definir *setDelayAdLoading* true se estiver usando um resolvedor personalizado.
>
