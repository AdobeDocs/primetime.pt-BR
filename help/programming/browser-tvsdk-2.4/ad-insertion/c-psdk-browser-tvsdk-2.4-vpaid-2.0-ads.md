---
description: A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele oferece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Suporte a anúncios VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Suporte a anúncios VPAID 2.0 {#vpaid-ad-support}

A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele oferece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são compatíveis:

* Versão 2.0 da especificação VPAID

  Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/guidelines/digital-video-player-ad-interface-definition-vpaid-2-0/).
* Anúncios lineares de VPAID com conteúdo de vídeo sob demanda (VOD)
* No conteúdo Ao vivo, o TVSDK do navegador é compatível com anúncios JavaScript VPAID precedentes.
* No modo de fallback do Flash, o TVSDK do navegador é compatível somente com anúncios VPAID baseados em Flashes.
* Anúncios JavaScript VPAID lineares

  Os anúncios VPAID devem ser baseados em JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são suportados:

* Versão 1.0 da especificação VPAID
* Anúncios ignoráveis
* Anúncios não lineares, como anúncios sobrepostos, anúncios complementares dinâmicos, anúncios minimizáveis, anúncios recolhíveis e anúncios expansíveis.
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios VPAID do Flash

## API {#section_0DB1D383CA5047B281BC808BC082C69B}

Os seguintes elementos de API são compatíveis com anúncios VPAID 2.0:

* A variável `getCustomAdView` método de `MediaPlayer` retorna um `CustomAdView` objeto, que representa a exibição da Web que renderiza o anúncio VPAID.

  Para obter mais informações sobre o `getCustomAdView` , consulte [Documentação da API do MediaPlayer](https://help.adobe.com/en_US/primetime/api/psdk/browser_tvsdk/AdobePSDK.MediaPlayer.html).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` define o tempo limite no processo de carregamento de VPAID.

  O valor de tempo limite padrão é de 10 segundos.

* A API, `auditudeSettings.ignoreVPAIDAds`, permite ignorar anúncios VPAID recebidos do servidor Auditude. A API não funciona para o fallback do Flash.

Enquanto o anúncio VPAID está sendo reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do reprodutor, de modo que o código que depende dos toques dos usuários na exibição do reprodutor não funciona.
* Chamadas para pausar e reproduzir na instância do player pausar e retomar o anúncio VPAID.
* Os anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

  A duração do anúncio e a duração total do ad break especificadas na resposta do servidor de publicidade podem não ser precisas.
