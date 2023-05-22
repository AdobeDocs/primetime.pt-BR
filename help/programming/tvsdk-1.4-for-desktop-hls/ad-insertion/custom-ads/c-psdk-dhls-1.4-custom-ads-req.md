---
description: A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) fornece uma interface comum para reproduzir anúncios de vídeo. O VPAID fornece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Requisitos para anúncios personalizados
exl-id: c13748d6-23f1-4f34-95b4-7b532db6e536
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Requisitos para anúncios personalizados {#custom-ad-requirements}

O reprodutor TVSDK pode reproduzir anúncios VPAID (Digital Video Player Ad-Interface Definition) e exibir o status de carregamento dos anúncios. Se houver erros no anúncio ou se os anúncios estiverem demorando muito para serem carregados, o TVSDK ignorará esses anúncios.

A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) fornece uma interface comum para reproduzir anúncios de vídeo. O VPAID fornece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

<!--<a id="section_9A358902CBC24999BA34206EE2029616"></a>-->

O TVSDK é compatível com os seguintes recursos:

* Versões 1.0 e 2.0 da especificação VPAID
* Anúncios lineares de VPAID em conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID do Flash

   Os anúncios VPAID devem ser baseados em Flashes e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/x-shockwave-flash`.

Os seguintes recursos não são suportados:

* Anúncios não lineares, como anúncios de sobreposição e anúncios complementares dinâmicos
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios de JavaScript VPAID

## Carregando status {#section_5F55C0101CD44A65BCFE1D124CBDF239}

O TVSDK despacha os seguintes eventos:

* `AdLoading`
* `AdLoaded`
* `AdStarted`
* `AdPlaying`
* `AdStopped`

Depois que a variável `AdStopped` evento, o TVSDK retomará o conteúdo do vídeo.

>[!TIP]
>
>Se você especificar um valor zero, o TVSDK tentará carregar o anúncio até que ele seja carregado ou até que um erro tenha ocorrido.

## Ignorando anúncios {#section_3EA452F420884335AE90DF23C17E416A}

Se o anúncio demorar muito para ser carregado ou houver erros no anúncio, o TVSDK poderá ignorar o anúncio e o próximo anúncio no pod de anúncio será reproduzido automaticamente.

Se a variável `AuditudeSettings.customAdLoadTimeout` Especifica um número de segundos maior que zero, o TVSDK tenta carregar o anúncio para a duração especificada. Se não conseguir carregar o anúncio, o anúncio é ignorado. Por exemplo, se você configurar `AuditudeSettings.customAdLoadTimeout:5`, o TVSDK tentará carregar o anúncio por no máximo 5 segundos. Se o anúncio ainda não carregar, ele será ignorado.
