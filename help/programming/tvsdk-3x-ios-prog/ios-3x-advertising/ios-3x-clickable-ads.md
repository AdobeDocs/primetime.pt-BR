---
description: O TVSDK fornece informações para que você possa agir em anúncios de click-through. À medida que você cria a interface do usuário do player, é necessário decidir como responder quando um usuário clica em um anúncio clicável.
seo-description: O TVSDK fornece informações para que você possa agir em anúncios de click-through. À medida que você cria a interface do usuário do player, é necessário decidir como responder quando um usuário clica em um anúncio clicável.
seo-title: Anúncios clicáveis
title: Anúncios clicáveis
uuid: 8b257483-8b90-47cf-be2a-095b6d5b8883
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Anúncios clicáveis {#clickable-ads}

O TVSDK fornece informações para que você possa agir em anúncios de click-through. À medida que você cria a interface do usuário do player, é necessário decidir como responder quando um usuário clica em um anúncio clicável.

No TVSDK para iOS, somente anúncios lineares podem ser clicados.

## Responder a cliques em anúncios {#section_537AF2593FDB4257B81AAE2103B0C719}

Quando um usuário clica em um anúncio, em um anúncio de banner complementar ou em um botão relacionado, seu aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.

1. Para configurar um ouvinte de evento para TVSDK e fornecer as informações de click-through, adicione um observador para `PTMediaPlayerAdClickNotification`.

   >[!NOTE]
   >
   >Quando um usuário clica em um anúncio, em um anúncio de banner complementar ou em um botão relacionado, o TVSDK envia essa notificação, incluindo informações sobre o destino do clique.

1. Monitore as interações do usuário em anúncios clicáveis.
1. Quando o usuário toca ou clica no anúncio ou botão, para notificar o TVSDK, use `[_player notifyClick:_currentAd.primaryAsset];`.
1. Analise o `PTMediaPlayerAdClickNotification` evento do TVSDK.
1. Para recuperar o URL de click-through e as informações relacionadas, use o `PTMediaPlayerAdClickURLKey` objeto.
1. Pause o vídeo.
1. Use as informações de click-through para exibir o URL de click-through do anúncio e as informações relacionadas.

   >[!NOTE]
   >
   >Você pode, por exemplo, exibir as informações de uma das seguintes maneiras:

   * Em seu aplicativo, abrindo o URL de click-through em um navegador.

      Em plataformas de desktop, a área de reprodução de vídeo e anúncio é usada para invocar URLs de click-through nos cliques do usuário.
   * Redirecione os usuários para seu navegador móvel externo.

      Em dispositivos móveis, a área de reprodução do anúncio de vídeo é usada para outras funções, como ocultar e mostrar controles, pausar a reprodução, expandir para tela cheia e assim por diante. Nesses dispositivos, uma exibição separada, como um botão patrocinador, é usada para iniciar o URL de click-through.

1. Feche a janela do navegador na qual as informações de click-through são exibidas e retome a reprodução do vídeo.

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
