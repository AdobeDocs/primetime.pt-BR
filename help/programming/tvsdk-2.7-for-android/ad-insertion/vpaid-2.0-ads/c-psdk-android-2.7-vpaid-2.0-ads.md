---
description: A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele oferece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Suporte a anúncios VPAID 2.0
exl-id: 24146e32-9021-4472-94f6-b3d4703f0f9a
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Suporte a anúncios VPAID 2.0 {#vpaid-ad-support}

A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele oferece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são compatíveis:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anúncios lineares de VPAID com conteúdo de vídeo sob demanda (VOD)
* Anúncios de JavaScript VPAID

   Os anúncios VPAID devem ser baseados em JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são suportados:

* Versão 1.0 da especificação VPAID
* Anúncios ignoráveis
* Anúncios não lineares, como anúncios de sobreposição, anúncios complementares dinâmicos, anúncios minimizáveis, anúncios recolhíveis e anúncios expansíveis
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios VPAID do Flash

## API

Os seguintes elementos de API são compatíveis com anúncios VPAID 2.0:

* A variável `getCustomAdView` método de `MediaPlayer` retorna um `CustomAdView` objeto, representando a exibição da Web que renderiza o anúncio VPAID (consulte [Referências da API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc/index.html)).

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` define o tempo limite no processo de carregamento de VPAID. O valor de tempo limite padrão é de 10 segundos.

Enquanto o anúncio VPAID está sendo reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do reprodutor, de modo que o código que depende dos toques dos usuários na exibição do reprodutor não funciona.
* Chamadas para `pause` e `play` na instância do reprodutor, pause e retome o anúncio VPAID.

* Os anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total do ad break especificadas na resposta do servidor de publicidade podem não ser precisas.
