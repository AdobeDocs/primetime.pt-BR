---
description: Quando os usuários avançam ou recuam rapidamente pela mídia, eles estão no modo de peça. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer com um valor diferente de 1.
title: Implementar rapidamente para a frente e retroceder
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---


# Visão geral {#implement-fast-forward-and-rewind-overview}

Quando os usuários avançam ou recuam rapidamente pela mídia, eles estão no modo de peça. Para entrar no modo de reprodução de truque, é necessário definir a taxa de reprodução do MediaPlayer com um valor diferente de 1.

Para alternar a velocidade, é necessário definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de reprodução por engano, definindo a taxa no `MediaPlayer` para um valor permitido.

   * A classe `MediaPlayerItem` define as taxas de reprodução permitidas.
   * TVSDK seleciona a taxa mais próxima permitida se a taxa especificada não for permitida.

   Este exemplo define a taxa de reprodução interna do reprodutor para a taxa solicitada.

   ```java
   import com.adobe.mediacore.MediaPlayer; 
   import com.adobe.mediacore.MediaPlayerItem; 
   import com.adobe.mediacore.MediaPlayerException; 
   import java.util.List; 
   import java.lang.Float; 
   
   private boolean setPlaybackRate(MediaPlayer player, float rate) throws MediaPlayerException  
   { 
       //Get list of playback rates that the media player supports 
       MediaPlayerItem item = player.getCurrentItem(); 
       if(item == null) return false; 
       List<Float> availableRates = player.getCurrentItem().getAvailablePlaybackRates(); 
   
       //Return false if requested rate is not supported 
       if(availableRates.indexOf(rate) == -1) return false; 
   
       //Otherwise set the playback rate to the requested rate  
       //(this can throw MediaPlayerException) 
       player.setRate(rate); 
       return true; 
   }
   ```

1. Opcionalmente, é possível acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente ocorre.

       O TVSDK despacha os seguintes eventos relacionados à reprodução de truque:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando o  `rate` valor muda para um valor diferente.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando a reprodução é retomada na taxa selecionada.

      O TVSDK despacha ambos os eventos quando o reprodutor volta do modo de trick-play para o modo de reprodução normal.

