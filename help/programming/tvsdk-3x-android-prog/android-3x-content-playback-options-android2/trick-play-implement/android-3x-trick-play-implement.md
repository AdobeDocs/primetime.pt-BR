---
description: Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, defina a taxa de reprodução do MediaPlayer para um valor diferente de 1.
title: Implementar avanço e retrocesso rápidos
exl-id: 9e2dd250-a86d-4d75-8eba-385624af17af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '201'
ht-degree: 0%

---

# Visão geral {#implement-fast-forward-and-rewind}

Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, defina a taxa de reprodução do MediaPlayer para um valor diferente de 1.

Para alternar a velocidade, você deve definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de truque de reprodução, definindo a taxa no `MediaPlayer` para um valor permitido.

       Lembre-se das seguintes informações:
   
   * A variável `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK seleciona a taxa permitida mais próxima se a taxa especificada não for permitida.

      O exemplo a seguir define a taxa de reprodução interna do reprodutor para a taxa solicitada:

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

1. Opcionalmente, você pode acompanhar eventos de alteração de taxa, que notificam quando você solicitou uma alteração de taxa e quando a alteração de taxa realmente ocorre.

O TVSDK despacha os seguintes eventos que estão relacionados com a reprodução:

* `MediaPlayerEvent.RATE_SELECTED`, quando a variável `rate` O valor de é alterado para um valor diferente.

* `MediaPlayerEvent.RATE_PLAYING`, quando a reprodução continua na taxa selecionada.

   O TVSDK despacha esses eventos quando o reprodutor retorna do modo de reprodução de truque para o modo de reprodução normal.
