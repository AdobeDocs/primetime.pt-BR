---
description: A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores obtenham anúncios de melhor público alvo, acompanhem impressões de anúncios e monetizem conteúdo de vídeo.
seo-description: A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores obtenham anúncios de melhor público alvo, acompanhem impressões de anúncios e monetizem conteúdo de vídeo.
seo-title: Suporte a anúncios VPAID 2.0
title: Suporte a anúncios VPAID 2.0
uuid: 6485e387-2a13-476f-a0fd-91c6e19fd385
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 0%

---


# Suporte a anúncios VPAID 2.0 {#vpaid-ad-support}

A definição de interface de serviço de anúncios (VPAID) 2.0 do player de vídeo fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores obtenham anúncios de melhor público alvo, acompanhem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são suportados:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anúncios VPAID lineares com conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID do JavaScript

   Os anúncios VPAID devem ter como base JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são suportados:

* Versão 1.0 da especificação VPAID
* Anúncios captáveis
* Anúncios não lineares, como anúncios sobrepostos, anúncios companheiros dinâmicos, anúncios minimizáveis, anúncios que podem ser recolhidos e anúncios expansíveis
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ativo
* Anúncios VPAID do Flash

## API

Os seguintes elementos de API suportam anúncios VPAID 2.0:

* O método `getCustomAdView` de `MediaPlayer` retorna um objeto `CustomAdView`, representando a visualização da Web que renderiza o anúncio VPAID (consulte [Referências de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` define o tempo limite no processo de carregamento VPAID. O valor de tempo limite padrão é de 10 segundos.

Enquanto o anúncio VPAID está sendo reproduzido:

* O anúncio VPAID é exibido em uma container de visualização acima da visualização do player, de modo que o código que depende de toques dos usuários na visualização do player não funciona.
* Chama `pause` e `play` na instância do player para pausar e retomar o anúncio VPAID.

* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total da quebra do anúncio especificados na resposta do servidor de anúncios podem não ser precisas.