---
description: A definição de interface de veiculação de anúncios (VPAID) 2.0 do reprodutor de vídeo oferece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Suporte a anúncio VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---


# Suporte a anúncio VPAID 2.0 {#vpaid-ad-support}

A definição de interface de veiculação de anúncios (VPAID) 2.0 do reprodutor de vídeo oferece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são compatíveis:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Anúncios VPAID lineares com conteúdo de vídeo sob demanda (VOD)
* No conteúdo ao vivo, o TVSDK do navegador é compatível com anúncios VPAID do JavaScript antes da exibição.
* No modo de fallback de Flash, o TVSDK do navegador é compatível somente com anúncios VPAID baseados em Flashes.
* Anúncios VPAID do JavaScript linear

   Os anúncios VPAID devem ser baseados em JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são compatíveis:

* Versão 1.0 da especificação VPAID
* Anúncios evitáveis
* Anúncios não lineares, como sobreposições, anúncios companheiros dinâmicos, anúncios minimizáveis, anúncios que podem ser recolhidos e anúncios expansíveis.
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios VPAID do Flash

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

Os seguintes elementos de API são compatíveis com anúncios VPAID 2.0:

* O método `getCustomAdView` de `MediaPlayer` retorna um objeto `CustomAdView`, que representa a exibição da Web que renderiza o anúncio VPAID.

   Para obter mais informações sobre o método `getCustomAdView`, consulte a [documentação da API do MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` define o tempo limite no processo de carregamento VPAID.

   O valor padrão do tempo limite é de 10 segundos.

* A API, `auditudeSettings.ignoreVPAIDAds`, permite ignorar anúncios VPAID recebidos do servidor Auditude. A API não funciona para o Fallback do Flash.

Enquanto o anúncio VPAID é reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do reprodutor, de modo que o código que depende de toques dos usuários na exibição do reprodutor não funciona.
* Chamadas para pausar e reproduzir na instância do reprodutor e retomar o anúncio VPAID.
* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total do ad break especificados na resposta do servidor de anúncios podem não ser precisas.