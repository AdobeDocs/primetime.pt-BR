---
description: A definição de interface de veiculação de anúncios (VPAID) 2.0 do reprodutor de vídeo oferece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Suporte a anúncio VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# Suporte a anúncio VPAID 2.0 {#vpaid-ad-support}

A definição de interface de veiculação de anúncios (VPAID) 2.0 do reprodutor de vídeo oferece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são compatíveis:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anúncios VPAID lineares no conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID do JavaScript

   Os anúncios VPAID devem ser baseados em JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são compatíveis:

* Versão 1.0 da especificação VPAID
* Anúncios evitáveis
* Anúncios não lineares, como sobreposições, anúncios companheiros dinâmicos, anúncios minimizáveis, anúncios que podem ser recolhidos e anúncios expansíveis
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios VPAID do Flash

## Alterações na API {#section_D62F3E059C6C493592D34534B0BFC150}

As seguintes alterações foram feitas à API:

* Uma função `getCustomAdView` foi adicionada em `MediaPlayer` e retorna a exibição da Web que renderiza o anúncio VPAID.

   Para obter mais informações sobre o objeto `CustomAdView` retornado por essa função, consulte [Referências de API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* Um evento `CUSTOM_AD` é despachado da instância do reprodutor de mídia.

   O aplicativo pode registrar um retorno de chamada de evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` permite alterar o tempo limite padrão no processo de carregamento do VPAID.

   O valor padrão do tempo limite é de 10 segundos.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Enquanto o anúncio VPAID é reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do reprodutor, de modo que o código que depende de toques dos usuários na exibição do reprodutor não funciona.
* O reprodutor de conteúdo principal é pausado e as chamadas para `pause` e `play` na instância do reprodutor são usadas para pausar e retomar o anúncio VPAID.

* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total do ad break definidas pela resposta do servidor de anúncio podem não ser precisas.

## Implementar a integração do VPAID 2.0 {#implement-vpaid-integration}

Para adicionar suporte ao VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

Para adicionar suporte ao VPAID 2.0:

1. Adicione a visualização de anúncio personalizada à interface do reprodutor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Adicione um ouvinte para eventos de anúncio personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
