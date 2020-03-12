---
description: A definição de interface de veiculação de anúncios (VPAID) do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. A VPAID fornece uma experiência de mídia avançada para usuários e permite que os editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
seo-description: A definição de interface de veiculação de anúncios (VPAID) do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. A VPAID fornece uma experiência de mídia avançada para usuários e permite que os editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
seo-title: Requisitos de anúncio personalizado
title: Requisitos de anúncio personalizado
uuid: 6d4ba87b-ffe5-467d-8ab5-9795928c2f69
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Requisitos de anúncio personalizado {#custom-ad-requirements}

O player TVSDK pode reproduzir anúncios VPAID (Ad-Interface Definition) digitais do player de vídeo e exibir o status de carregamento do anúncio. Se houver erros no anúncio ou se os anúncios estiverem demorando muito para serem carregados, o TVSDK ignorará esses anúncios.

A definição de interface de veiculação de anúncios (VPAID) do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. A VPAID fornece uma experiência de mídia avançada para usuários e permite que os editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

O TVSDK oferece suporte aos seguintes recursos:

* Versão 1.0 e 2.0 da especificação VPAID
* Anúncios VPAID lineares em conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID Flash

   Os anúncios VPAID devem ser baseados em Flash e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/x-shockwave-flash`.

Os seguintes recursos não são suportados:

* Anúncios não lineares, como anúncios sobrepostos e anúncios companheiros dinâmicos
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ativo
* Anúncios VPAID do JavaScript

## Carregando status {#section_5F55C0101CD44A65BCFE1D124CBDF239}

O TVSDK envia os seguintes eventos:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Após o `AdStopped` evento, o TVSDK retoma o conteúdo do vídeo.

>[!TIP]
>
>Se você especificar um valor de zero, o TVSDK tentará carregar o anúncio até que ele seja carregado ou ocorrer um erro.

## Ignorando anúncios {#section_3EA452F420884335AE90DF23C17E416A}

Se o anúncio demorar muito para carregar ou se houver erros no anúncio, o TVSDK poderá ignorar o anúncio e o próximo anúncio no pod de anúncio será reproduzido automaticamente.

Se a `AuditudeSettings.customAdLoadTimeout` configuração especificar um número de segundos maior que zero, o TVSDK tentará carregar o anúncio com a duração especificada. Se ele não conseguir carregar o anúncio, ele será ignorado. Por exemplo, se você configurar `AuditudeSettings.customAdLoadTimeout:5`, o TVSDK tentará carregar o anúncio por um máximo de 5 segundos. Se o anúncio ainda não for carregado, ele será ignorado.
