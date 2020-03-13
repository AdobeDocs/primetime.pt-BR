---
description: A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
seo-description: A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
seo-title: Suporte a anúncios VPAID 2.0
title: Suporte a anúncios VPAID 2.0
uuid: e45e91d2-2aef-4d69-ac80-228d23e8fd7b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Visão geral {#vpaid-ad-support-overview}

A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são suportados:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anúncios VPAID lineares com conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID do JavaScript

   Os anúncios VPAID devem ter como base o JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são suportados:

* Versão 1.0 da especificação VPAID
* Anúncios captáveis
* Anúncios não lineares, como anúncios sobrepostos, anúncios companheiros dinâmicos, anúncios minimizáveis, anúncios que podem ser recolhidos e anúncios expansíveis
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ativo
* Anúncios VPAID Flash

## API

Os seguintes elementos de API suportam anúncios VPAID 2.0:

* O `getCustomAdView` método de `MediaPlayer` retorna um `CustomAdView` objeto, representando a exibição da Web que renderiza o anúncio VPAID (consulte Referências [de](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)API).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` define o tempo limite no processo de carregamento VPAID. O valor de tempo limite padrão é de 10 segundos.

Enquanto o anúncio VPAID está sendo reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do player, de modo que o código que depende de toques dos usuários na exibição do player não funciona.
* Chama para `pause` e `play` na instância do player pausar e retomar o anúncio VPAID.

* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total da quebra do anúncio especificados na resposta do servidor de anúncios podem não ser precisas.