---
description: Você pode ativar ou desativar o recurso Resolução de anúncio lento usando o mecanismo de Carregamento de anúncio lento existente (A Resolução de anúncio lento é ativada por padrão).
keywords: Lento;Resolução de anúncio;Carregamento de anúncio;delayLoading
title: Habilitar resolução de anúncios lentos
exl-id: 4cd53ace-b0f5-4eef-93c3-644c2f48ce49
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---

# Habilitar resolução de anúncios lentos {#enable-lazy-ad-resolving}

Você pode ativar ou desativar o recurso Resolução de anúncio lento usando o mecanismo de Carregamento de anúncio lento existente (A Resolução de anúncio lento é ativada por padrão).

Você pode ativar ou desativar a Resolução de anúncios lentos chamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) com `true` ou `false`.

1. Usar o booleano `hasDelayAdLoading` e `setDelayAdLoading` métodos em `AdvertisingMetadata` para controlar o tempo de resolução do anúncio e o posicionamento dos anúncios na linha do tempo:

   * Se `hasDelayAdLoading` retorna false, o TVSDK aguarda até que todos os anúncios sejam resolvidos e colocados antes da transição para o estado PREPARADO.
   * Se `hasDelayAdLoading` retorna true, o TVSDK resolve somente os anúncios iniciais e faz a transição para o estado PREPARADO. Os anúncios restantes são resolvidos e colocados durante a reprodução.
   * Quando `hasPreroll` ou `hasLivePreroll` Quando retornado como false, o TVSDK presume que não há anúncio precedente e inicia a reprodução do conteúdo imediatamente. O padrão é true.

      APIs relevantes para resolução de anúncios lentos:

      ```
      Class: 
         com.adobe.mediacore.metadata.AdvertisingMetadata 
      
      Methods: 
      […] 
          public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
          public final void setDelayAdLoading()    // Enable or disable Lazy Ad Resolving 
          public final boolean hasPreroll()        // Check for existence of pre-roll ads 
          public final void setPreroll()           // Set pre-roll true or false 
          public final boolean hasLivePreroll()    // Check for live pre-roll ads 
          public final void setLivePreroll()       // Set live pre-roll true or false 
      […]
      ```

1. Para refletir com precisão os anúncios como dicas em uma barra de limpeza, acompanhe o `TimelineEvent` e redesenhe a barra de limpeza toda vez que receber esse evento.

   Quando a Resolução de anúncios ociosos está ativada para fluxos de VOD, nem todos os anúncios são colocados na linha do tempo quando o reprodutor entra no estado PREPARADO, portanto, o reprodutor deve redesenhar explicitamente a barra de limpeza.

   O TVSDK otimiza o despacho desse evento para minimizar o número de vezes que você deve redesenhar a barra de depuração; portanto, o número de eventos na linha do tempo não está relacionado ao número de ad breaks a serem colocados na linha do tempo. Por exemplo, se você tiver cinco ad breaks, talvez não receba exatamente cinco eventos.

   ```java
   mediaPlayer.addEventListener 
       (MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
   /** 
    * ... 
    */ 
   public void onTimelineUpdated(TimelineEvent event) { 
   
       for (PlaybackManagerEventListener listener : eventListeners) { 
           listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
       } 
   } 
   ```

>Para verificar se o recurso de Resolução de anúncio lento está ativado ou desativado, chame `AdvertisingMetadata.hasDelayAdLoading`. Um valor de retorno de `true` significa que a Resolução de anúncios ociosos está ativada; `false` significa que o recurso está desativado.
