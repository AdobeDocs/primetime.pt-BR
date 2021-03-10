---
description: Você pode ativar ou desativar o recurso de Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçosos (a Resolução de anúncios preguiçosos é ativada por padrão).
keywords: Preguiçoso;Resolução de anúncio;Carregamento de anúncio;delayLoading
title: Habilitar a resolução de anúncio lento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 0%

---


# Habilitar lento e resolver {#enable-lazy-ad-resolving}

Você pode ativar ou desativar o recurso de Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçosos (a Resolução de anúncios preguiçosos é ativada por padrão).

Você pode ativar ou desativar a Resolução de anúncio preguiçoso ao chamar [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) com `true` ou `false`.

1. Use os métodos Booleano `hasDelayAdLoading` e `setDelayAdLoading` em `AdvertisingMetadata` para controlar o tempo da resolução do anúncio e o posicionamento dos anúncios na linha do tempo:

   * Se `hasDelayAdLoading` retornar falso, o TVSDK aguarda até que todos os anúncios sejam resolvidos e colocados antes da transição para o estado PREPARADO.
   * Se `hasDelayAdLoading` retornar true, o TVSDK resolverá apenas os anúncios iniciais e fará a transição para o estado PREPARADO. Os anúncios restantes são resolvidos e colocados durante a reprodução.
   * Quando `hasPreroll` ou `hasLivePreroll` retornar falso, o TVSDK assume que não há um anúncio de pré-lançamento e inicia a reprodução do conteúdo imediatamente. O padrão é true.

      APIs relevantes para a resolução de anúncios lentos:

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

1. Para refletir com precisão os anúncios como dicas em uma barra de depuração, escute o evento `TimelineEvent` e redesenhe a barra de depuração sempre que receber esse evento.

   Quando a resolução de anúncios ociosos está ativada para fluxos VOD, nem todos os anúncios são colocados na linha do tempo quando o reprodutor entra no estado PREPARADO, de modo que o reprodutor deve redesenhar explicitamente a barra de depuração.

   O TVSDK otimiza o despacho desse evento para minimizar o número de vezes que você deve redesenhar a barra de depuração; portanto, o número de eventos de linha do tempo não está relacionado ao número de ad breaks a serem colocados na linha do tempo. Por exemplo, se você tiver cinco ad breaks, talvez você não receba exatamente cinco eventos.

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

>Para verificar se o recurso de Resolução de Anúncios Preguiçosos está ativado ou desativado, chame `AdvertisingMetadata.hasDelayAdLoading`. Um valor de retorno de `true` significa que a Resolução de Anúncios Preguiçosos está ativada; `false` significa que o recurso está desativado.

