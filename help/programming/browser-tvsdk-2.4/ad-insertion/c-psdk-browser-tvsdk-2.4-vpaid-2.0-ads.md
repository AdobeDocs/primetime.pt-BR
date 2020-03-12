---
description: A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
seo-description: A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
seo-title: Suporte a anúncios VPAID 2.0
title: Suporte a anúncios VPAID 2.0
uuid: 462692b5-c4b3-4488-adb3-f309809d64ad
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Suporte a anúncios VPAID 2.0 {#vpaid-ad-support}

A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são suportados:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Anúncios VPAID lineares com conteúdo de vídeo sob demanda (VOD)
* No conteúdo ao vivo, o TVSDK do navegador oferece suporte a anúncios anteriores do JavaScript VPAID.
* No modo de fallback Flash, o TVSDK do navegador suporta apenas anúncios VPAID baseados em Flash.
* Anúncios VPAID do JavaScript linear

   Os anúncios VPAID devem ter como base o JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são suportados:

* Versão 1.0 da especificação VPAID
* Anúncios captáveis
* Anúncios não lineares, como sobreposições, anúncios companheiros dinâmicos, anúncios minimizáveis, anúncios que podem ser recolhidos e anúncios expansíveis.
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ativo
* Anúncios VPAID Flash

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

Os seguintes elementos de API suportam anúncios VPAID 2.0:

* O `getCustomAdView` método de `MediaPlayer` retorna um `CustomAdView` objeto, que representa a exibição da Web que renderiza o anúncio VPAID.

   Para obter mais informações sobre o `getCustomAdView` método, consulte a documentação [da API do](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html)MediaPlayer.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` define o tempo limite no processo de carregamento VPAID.

   O valor de tempo limite padrão é de 10 segundos.

* A API, `auditudeSettings.ignoreVPAIDAds`, permite que você ignore os anúncios VPAID recebidos do servidor Auditude. A API não funciona para o Flash Fallback.

Enquanto o anúncio VPAID está sendo reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do player, de modo que o código que depende de toques dos usuários na exibição do player não funciona.
* Chama para pausar e reproduzir na instância do player pausar e retomar o anúncio VPAID.
* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total da quebra do anúncio especificados na resposta do servidor de anúncios podem não ser precisas.