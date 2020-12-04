---
description: O Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores obtenham anúncios de melhor público alvo, acompanhem impressões de anúncios e monetizem conteúdo de vídeo.
seo-description: O Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores obtenham anúncios de melhor público alvo, acompanhem impressões de anúncios e monetizem conteúdo de vídeo.
seo-title: Suporte a anúncios VPAID 2.0
title: Suporte a anúncios VPAID 2.0
uuid: b688d244-c5ac-4832-b5c2-cb25bc80ce8b
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---


# Suporte a anúncios VPAID 2.0 {#vpaid-ad-support}

O Video Player Ad-Serving Interface Definition (VPAID) 2.0 fornece uma interface comum para reproduzir anúncios de vídeo. Ele fornece uma experiência de mídia avançada para usuários e permite que editores obtenham anúncios de melhor público alvo, acompanhem impressões de anúncios e monetizem conteúdo de vídeo.

Os seguintes recursos são suportados:

* Versão 2.0 da especificação VPAID

   Para obter mais informações, consulte [IAB VPAID 2.0](https://www.iab.com/wp-content/uploads/2015/06/VPAID_2_0_Final_04-10-2012.pdf).
* Anúncios VPAID lineares em conteúdo de vídeo sob demanda (VOD)
* Anúncios VPAID do JavaScript

   Os anúncios VPAID devem ter como base JavaScript e a resposta do anúncio deve identificar o tipo de mídia do anúncio VPAID como `application/javascript`.

Os seguintes recursos não são suportados:

* Versão 1.0 da especificação VPAID
* Anúncios captáveis
* Anúncios não lineares, como anúncios sobrepostos, anúncios companheiros dinâmicos, anúncios minimizáveis, anúncios desdobráveis e anúncios expansíveis
* Pré-carregamento de anúncios VPAID
* Anúncios VPAID em conteúdo ativo
* Anúncios VPAID do Flash
* Anúncio VPAID pós-rolagem

## Alterações da API {#section_D62F3E059C6C493592D34534B0BFC150}

As seguintes alterações foram feitas na API:

* `PTAuditudeMetadata` tem uma  `customAdLoadTimeout` propriedade para alterar o tempo limite padrão no processo de carregamento VPAID.

   O valor de tempo limite padrão é de 10 segundos.

* `PTMediaPlayerCustomAdNotification` é despachado da  `PTMediaPlayer` instância

<!--<a id="section_495700E1C5404A7B85307A4137C740C5"></a>-->

Enquanto o anúncio VPAID está sendo reproduzido:

* O anúncio VPAID é exibido em uma container de visualização acima da visualização do player, de modo que o código que depende de toques dos usuários na visualização do player não funciona.
* O player de conteúdo principal está pausado e as chamadas para `pause` e `play` na instância do player são usadas para pausar e retomar o anúncio VPAID.

* Anúncios VPAID não têm uma duração predefinida, pois o anúncio pode ser interativo.

   A duração do anúncio e a duração total do intervalo do anúncio, definidas pela resposta do servidor de anúncios, podem não ser precisas.

## Implementação da integração com VPAID 2.0 {#section_63C9C737367C4A0AB4D62E0DC2084141}

Para adicionar suporte a VPAID 2.0 em seu aplicativo iOS:

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
