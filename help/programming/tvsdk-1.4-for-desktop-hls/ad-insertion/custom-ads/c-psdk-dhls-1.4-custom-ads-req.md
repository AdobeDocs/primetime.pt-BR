---
description: A definição de interface de veiculação de anúncios (VPAID) do reprodutor de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. O VPAID fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Requisitos do anúncio personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Requisitos de anúncio personalizado {#custom-ad-requirements}

O reprodutor TVSDK pode reproduzir anúncios de definição de interface de anúncio (VPAID) do reprodutor de vídeo digital e exibir o status de carregamento do anúncio. Se houver erros no anúncio ou se os anúncios estiverem demorando muito para serem carregados, o TVSDK ignorará esses anúncios.

A definição de interface de veiculação de anúncios (VPAID) do reprodutor de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. O VPAID fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

O TVSDK é compatível com os seguintes recursos:

* Versão 1.0 e 2.0 da especificação VPAID
* Anúncios VPAID lineares no conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID do Flash

   Os anúncios VPAID devem ser baseados em Flashes, e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/x-shockwave-flash`.

Os seguintes recursos não são compatíveis:

* Anúncios não lineares, como anúncios de sobreposição e anúncios companheiros dinâmicos
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios VPAID do JavaScript

## Carregando status {#section_5F55C0101CD44A65BCFE1D124CBDF239}

O TVSDK despacha os seguintes eventos:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Após o evento `AdStopped` , o TVSDK retoma o conteúdo do vídeo.

>[!TIP]
>
>Se você especificar um valor zero, o TVSDK tentará carregar o anúncio até que ele seja carregado ou ocorrer um erro.

## Ignorando anúncios {#section_3EA452F420884335AE90DF23C17E416A}

Se o anúncio demorar muito para ser carregado ou houver erros no anúncio, o TVSDK pode ignorar o anúncio, e o próximo anúncio no pod de anúncio será reproduzido automaticamente.

Se a configuração `AuditudeSettings.customAdLoadTimeout` especificar um número de segundos maior que zero, o TVSDK tentará carregar o anúncio pela duração especificada. Se não conseguir carregar o anúncio, o anúncio será ignorado. Por exemplo, se você configurar `AuditudeSettings.customAdLoadTimeout:5`, o TVSDK tentará carregar o anúncio por um máximo de 5 segundos. Se o anúncio ainda não carregar, ele será ignorado.
