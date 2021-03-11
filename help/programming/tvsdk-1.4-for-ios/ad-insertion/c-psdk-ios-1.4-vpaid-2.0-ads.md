---
description: A definição de interface de veiculação de anúncios (VPAID) 2.0 do reprodutor de vídeo oferece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores direcionem melhor anúncios, rastreiem impressões de anúncios e monetizem conteúdo de vídeo.
title: Suporte a anúncio VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '323'
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
* Anúncio VPAID após a exibição

## Alterações na API {#section_D62F3E059C6C493592D34534B0BFC150}

As seguintes alterações foram feitas à API:

* `PTAuditudeMetadata` O tem uma  `customAdLoadTimeout` propriedade para alterar o tempo limite padrão no processo de carregamento de VPAID.

   O valor padrão do tempo limite é de 10 segundos.

* `PTMediaPlayerCustomAdNotification` é despachado da  `PTMediaPlayer` instância

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Enquanto o anúncio VPAID é reproduzido:

* O anúncio VPAID é exibido em um contêiner de exibição acima da exibição do reprodutor, de modo que o código que depende de toques dos usuários na exibição do reprodutor não funciona.
* O reprodutor de conteúdo principal é pausado e as chamadas para `pause` e `play` na instância do reprodutor são usadas para pausar e retomar o anúncio VPAID.

* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total do ad break definidas pela resposta do servidor de anúncio podem não ser precisas.

## Implementar a integração do VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Para adicionar suporte ao VPAID 2.0 no aplicativo iOS:

1. (Opcional) Adicione um ouvinte para eventos de anúncio personalizados.

   ```
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerCustomAdNotification:) name:PTMediaPlayerCustomAdNotification object:self.player];
   ```

1. (Opcional) Exiba a notificação.

   ```
   -(void)onMediaPlayerCustomAdNotification:(NSNotification *)notification{    PTCustomAdNotificationObject *notificationObject = [notification.userInfo objectForKey:PTCustomAdNotificationObjectKey];    if (notificationObject)    
   {        NSLog(@"ViewController:: Custom Ad Notification Received: %ld", notificationObject.type);    } 
   
   }
   ```

