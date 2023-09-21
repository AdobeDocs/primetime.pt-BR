---
description: O TVSDK fornece informações para que você possa agir em anúncios de click-through. Ao criar a interface do usuário do player, é necessário decidir como responder quando um usuário clicar em um anúncio clicável.
title: Anúncios clicáveis
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 0%

---

# Anúncios clicáveis{#clickable-ads}

O TVSDK fornece informações para que você possa agir em anúncios de click-through. Ao criar a interface do usuário do player, é necessário decidir como responder quando um usuário clicar em um anúncio clicável.

No TVSDK para iOS, somente anúncios lineares são clicáveis.

## Responder a cliques nos anúncios {#section_537AF2593FDB4257B81AAE2103B0C719}

Quando um usuário clica em um anúncio, em um anúncio de banner complementar ou em um botão relacionado, seu aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.

1. Para configurar um ouvinte de eventos para o TVSDK e fornecer as informações de click-through, adicione um observador para `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >Quando um usuário clica em um anúncio, em um banner complementar ou em um botão relacionado, o TVSDK envia essa notificação, incluindo informações sobre o destino do clique.

1. Monitore as interações do usuário em anúncios clicáveis.
1. Quando o usuário tocar ou clicar no anúncio ou botão, para notificar o TVSDK, use `[_player notifyClick:_currentAd.primaryAsset];`.
1. Ouça o `PTMediaPlayerAdClickNotification` evento do TVSDK.
1. Para recuperar o URL de click-through e informações relacionadas, use o `PTMediaPlayerAdClickURLKey` objeto.
1. Pausar o vídeo.
1. Use as informações de click-through para exibir o URL de click-through do anúncio e as informações relacionadas.

   >[!NOTE]
   >
   >Você pode, por exemplo, exibir as informações de uma das seguintes maneiras:

   * No aplicativo, abrindo o URL de click-through em um navegador.

     Em plataformas de desktop, a área de reprodução de anúncio de vídeo é usada para chamar URLs de click-through nos cliques do usuário.
   * Redirecione os usuários para seus navegadores web externos para dispositivos móveis.

     Em dispositivos móveis, a área de reprodução de anúncio de vídeo é usada para outras funções, como ocultar e mostrar controles, pausar a reprodução, expandir para tela inteira e assim por diante. Nesses dispositivos, uma exibição separada, como um botão patrocinador, é usada para iniciar o URL de click-through.

1. Feche a janela do navegador na qual as informações de click-through são exibidas e continue a reproduzir o vídeo.

   Por exemplo:

   ```
      // Listening for click notification  
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerAdClick:)  
    name:PTMediaPlayerAdClickNotification object:self.player]; 
   - (void) onMediaPlayerAdClick:(NSNotification *) notification { 
      NSString *url = [notification.userInfo objectForKey:PTMediaPlayerAdClickURLKey];  
      if (url != nil) { 
          [self openBrowser:[NSURL URLWithString:url]]; 
      } 
   } 
   ```
