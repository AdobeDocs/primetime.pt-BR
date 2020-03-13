---
description: Você pode ativar ou desativar o recurso Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está ativada por padrão).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Você pode ativar ou desativar o recurso Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está ativada por padrão).
seo-title: Ativar resolução de anúncios ociosos
title: Ativar resolução de anúncios ociosos
uuid: a084ee0b-53af-4600-91f6-d30ccc89699d
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Ativar resolução de anúncios ociosos {#enable-lazy-ad-resolving}

Você pode ativar ou desativar o recurso Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está ativada por padrão).

Você pode ativar ou desativar a Resolução de anúncios preguiçosos chamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) com `true` ou `false`.

1. Use os métodos Booliano `hasDelayAdLoading` e `setDelayAdLoading` Booleano em `AdvertisingMetadata` para controlar o tempo de resolução do anúncio e o posicionamento dos anúncios na linha do tempo:

   * Se `hasDelayAdLoading` retornar falso, o TVSDK aguarda até que todos os anúncios sejam resolvidos e colocados antes da transição para o estado PREPARADO.
   * Se `hasDelayAdLoading` retornar true, o TVSDK resolverá somente os anúncios e as transições iniciais para o estado PREPARADO. Os anúncios restantes são resolvidos e colocados durante a reprodução.
   * Quando `hasPreroll` ou `hasLivePreroll` retornar falso, o TVSDK assume que não há um anúncio pré-pago e inicia a reprodução do conteúdo imediatamente. O padrão é true.

      APIs relevantes para a resolução de anúncios ociosos:

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

1. Para refletir com precisão as publicidades como dicas em uma barra de depuração, escute o `TimelineEvent` evento e redesenhe a barra de depuração toda vez que receber esse evento.

   Quando a Resolução de anúncios ociosos está ativada para fluxos VOD, nem todos os anúncios são colocados na linha do tempo quando o player entra no estado PREPARADO, de modo que o player deve redesenhar explicitamente a barra de depuração.

   O TVSDK otimiza o despacho desse evento para minimizar o número de vezes que você deve redesenhar a barra de depuração; portanto, o número de eventos de linha do tempo não está relacionado ao número de quebras de anúncios a serem colocadas na linha do tempo. Por exemplo, se você tiver cinco pausas de anúncio, talvez você não receba exatamente cinco eventos.

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

>Para verificar se o recurso Resolução de anúncios ociosos está ativado ou desativado, faça uma chamada `AdvertisingMetadata.hasDelayAdLoading`. Um valor de retorno de `true` significa que a Resolução de anúncios preguiçosos está ativada; `false` significa que o recurso está desativado.

