---
description: A definição de interface de veiculação de anúncios (VPAID) 2.0 do reprodutor de vídeo oferece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Suporte a anúncio VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# Visão geral {#vpaid-ad-support-overview}

A definição de interface de veiculação de anúncios (VPAID) 2.0 do reprodutor de vídeo oferece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são compatíveis:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anúncios VPAID lineares com conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID do JavaScript

   Os anúncios VPAID devem ser baseados em JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são compatíveis:

* Versão 1.0 da especificação VPAID
* Anúncios evitáveis
* Anúncios não lineares, como sobreposições, anúncios companheiros dinâmicos, anúncios minimizáveis, anúncios que podem ser recolhidos e anúncios expansíveis
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios VPAID do Flash

## API

Os seguintes elementos de API são compatíveis com anúncios VPAID 2.0:

* O método `getCustomAdView` de `MediaPlayer` retorna um objeto `CustomAdView`, representando a exibição da Web que renderiza o anúncio VPAID (consulte [Referências de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` define o tempo limite no processo de carregamento VPAID. O valor padrão do tempo limite é de 10 segundos.

Enquanto o anúncio VPAID é reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do reprodutor, de modo que o código que depende de toques dos usuários na exibição do reprodutor não funciona.
* Chama `pause` e `play` na instância do reprodutor para e retoma o anúncio VPAID.

* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total do ad break especificados na resposta do servidor de anúncios podem não ser precisas.