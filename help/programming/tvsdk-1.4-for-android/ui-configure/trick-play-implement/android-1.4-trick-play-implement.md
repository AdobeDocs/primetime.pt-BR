---
description: Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.
title: Implementar avanço e retrocesso rápidos
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 0%

---

# Visão geral {#implement-fast-forward-and-rewind-overview}

Quando os usuários avançam ou retrocedem rapidamente pela mídia, eles estão no modo de execução. Para entrar no modo de execução de truque, é necessário definir a taxa de reprodução do MediaPlayer para um valor diferente de 1.

Para alternar a velocidade, você deve definir um valor.

1. Mova do modo de reprodução normal (1x) para o modo de truque de reprodução, definindo a taxa no `MediaPlayer` para um valor permitido.

   * A variável `MediaPlayerItem` define as taxas de reprodução permitidas.
   * O TVSDK seleciona a taxa permitida mais próxima se a taxa especificada não for permitida.

   Esse exemplo define a taxa de reprodução interna do reprodutor para a taxa solicitada.

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

1. Opcionalmente, você pode acompanhar eventos de alteração de taxa, que informam quando você solicitou uma alteração de taxa e quando uma alteração de taxa realmente ocorre.

       O TVSDK despacha os seguintes eventos relacionados ao trick play:
   
   * `AdobePSDK.PSDKEventType.RATE_SELECTED` quando a variável `rate` O valor de é alterado para um valor diferente.

   * `AdobePSDK.PSDKEventType.RATE_PLAYING` quando a reprodução continua na taxa selecionada.

     O TVSDK despacha ambos os eventos quando o reprodutor retorna do modo &quot;trick-play&quot; para o modo de reprodução normal.
