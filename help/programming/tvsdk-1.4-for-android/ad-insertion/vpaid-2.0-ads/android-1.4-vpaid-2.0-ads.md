---
description: A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele oferece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Suporte a anúncios VPAID 2.0
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---

# Suporte a anúncios VPAID 2.0 {#vpaid-ad-support}

A definição de interface de veiculação de anúncios do reprodutor de vídeo (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele oferece uma experiência de mídia avançada para os usuários e permite que os editores direcionem anúncios de maneira mais eficaz, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são compatíveis:

* Versão 2.0 da especificação VPAID

  Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anúncios lineares de VPAID em conteúdo de vídeo sob demanda (VOD)
* Anúncios de JavaScript VPAID

  Os anúncios VPAID devem ser baseados em JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são suportados:

* Versão 1.0 da especificação VPAID
* Anúncios ignoráveis
* Anúncios não lineares como anúncios de sobreposição, anúncios complementares dinâmicos, anúncios minimizáveis, anúncios recolhíveis e anúncios expansíveis
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ao vivo
* Anúncios VPAID do Flash

## Alterações na API {#section_D62F3E059C6C493592D34534B0BFC150}

As seguintes alterações foram feitas na API:

* A `getCustomAdView` a função foi adicionada em `MediaPlayer` e retorna a exibição da Web que renderiza o anúncio VPAID.

  Para obter mais informações sobre o `CustomAdView` que é retornado por esta função, consulte [Referências da API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/index.html).

* A `CUSTOM_AD` é despachado da instância do reprodutor de mídia.

  O aplicativo pode registrar um retorno de chamada de evento implementando `CustomAdEventListener`.

* `MediaPlayer.setCustomAdTimeout(int milliseconds)` permite alterar o tempo limite padrão no processo de carregamento do VPAID.

  O valor de tempo limite padrão é de 10 segundos.

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Enquanto o anúncio VPAID está sendo reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do reprodutor, de modo que o código que depende dos toques dos usuários na exibição do reprodutor não funciona.
* O reprodutor de conteúdo principal está pausado e chama `pause` e `play` na instância do reprodutor são usados para pausar e retomar o anúncio VPAID.

* Os anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

  A duração do anúncio e a duração total do ad break definidas pela resposta do servidor de publicidade podem não ser precisas.

## Implementar a integração com VPAID 2.0 {#implement-vpaid-integration}

Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

Para adicionar suporte a VPAID 2.0:

1. Adicione a exibição de anúncio personalizada à interface do reprodutor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Adicione um ouvinte para eventos de anúncio personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```
