---
description: Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, defina a taxa de reprodução do MediaPlayer para um valor diferente de 1.
seo-description: Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, defina a taxa de reprodução do MediaPlayer para um valor diferente de 1.
seo-title: Implementar para frente e retroceder rapidamente
title: Implementar para frente e retroceder rapidamente
uuid: d54c8c61-887f-4362-9085-e443859854b9
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---


# Visão geral {#implement-fast-forward-and-rewind}

Quando os usuários avançam rapidamente para a frente ou retrocedem rapidamente pela mídia, eles estão no modo trick play. Para entrar no modo de reprodução de truque, defina a taxa de reprodução do MediaPlayer para um valor diferente de 1.

Para mudar a velocidade, é necessário definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de reprodução de truque definindo a taxa em `MediaPlayer` para um valor permitido.

       Lembre-se das seguintes informações:
   
   * A classe `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK seleciona a taxa mais próxima permitida se a taxa especificada não for permitida.

      O exemplo a seguir define a taxa de reprodução interna do player para a taxa solicitada:

      ```
      import com.adobe.mediacore.MediaPlayer; 
      import com.adobe.mediacore.MediaPlayerItem; 
      import com.adobe.mediacore.MediaPlayerException; 
      import java.util.List; 
      import java.lang.Float; 
      
      private boolean setPlaybackRate(MediaPlayer player, float rate)  
        throws MediaPlayerException { 
          // Get list of playback rates that the media player supports 
          MediaPlayerItem item = player.getCurrentItem(); 
          if (item == null) return false; 
          List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
      
          // Return false if requested rate is not supported 
          if (availableRates.indexOf(rate) == -1) return false; 
      
          // Otherwise set the playback rate to the requested rate  
          // (this can throw MediaPlayerException) 
          player.setRate(rate); 
          return true; 
      }
      ```

1. Opcionalmente, você pode acompanhar eventos de alteração de taxa, o que informa quando você solicitou uma alteração de taxa e quando a alteração de taxa realmente ocorre.

O TVSDK despacha os seguintes eventos relacionados à reprodução de truques:

* `MediaPlayerEvent.RATE_SELECTED`, quando o  `rate` valor muda para um valor diferente.

* `MediaPlayerEvent.RATE_PLAYING`, quando a reprodução é retomada na taxa selecionada.

   O TVSDK despacha esses eventos quando o player retorna do modo de reprodução de truque para o modo de reprodução normal.