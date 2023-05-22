---
description: Você pode ativar ou desativar o recurso Resolução de anúncio lento usando o mecanismo de Carregamento de anúncio lento existente (A Resolução de anúncio lento está desativada por padrão).
keywords: Lento;Resolução de anúncio;Carregamento de anúncio;delayLoading
title: Habilitar resolução de anúncios lentos
exl-id: a52a1f9a-3bf6-4193-8347-1ef248ba8884
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---

# Habilitar resolução de anúncios lentos {#enable-lazy-ad-resolving}

Você pode ativar ou desativar o recurso Resolução de anúncio lento usando o mecanismo de Carregamento de anúncio lento existente (A Resolução de anúncio lento está desativada por padrão).

Você pode ativar ou desativar a Resolução de anúncios lentos chamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) com verdadeiro ou falso.

* Usar o booleano *hasDelayAdLoading* e *setDelayAdLoading* métodos em AdvertisingMetadata para controlar o tempo de resolução do anúncio e a colocação de anúncios na linha do tempo:

   * Se *hasDelayAdLoading* retorna false, o TVSDK aguarda até que todos os anúncios sejam resolvidos e colocados antes da transição para o estado PREPARADO.
   * Se *hasDelayAdLoading* retorna true, o TVSDK resolve somente os anúncios iniciais e faz a transição para o estado PREPARADO.

      * Os anúncios restantes são resolvidos e colocados durante a reprodução.
   * Quando *hasPreroll *ou *hasLivePreroll* Quando retornado como false, o TVSDK presume que não há anúncio precedente e inicia a reprodução do conteúdo imediatamente. Elas são definidas como true por padrão.


**APIs relevantes para resolução de anúncios lentos:**

```
Class:    com.adobe.mediacore.metadata.AdvertisingMetadata 
Methods: 
    public final boolean hasDelayAdLoading() // Check if Lazy Ad Resolving enabled 
    public final void setDelayAdLoading() // Enable or disable Lazy Ad Resolving 
    public final void setDelayAdLoadingTolerance() // Sets the Lazy Ad Resolving Tolerance level.  This value is added to the BufferControlParameters::playBufferTime and the content's EXT-X-TARGETDURATION to determine when ad breaks should resolve 
    public final double getDelayAdLoadingTolerance() // Gets the Lazy Ad Resolving Tolerance level 
    public final boolean hasPreroll() // Check for existence of pre-roll ads 
    public final void setPreroll() // Set pre-roll true or false 
    public final boolean hasLivePreroll() // Check for live pre-roll ads 
    public final void setLivePreroll() // Set live pre-roll true or false

Class:     com.adobe.mediacore.timeline.TimelineMarker 
Methods: 
    public double getDuration() // Returns the current duration of the TimelineMarker.  This will be zero if the ad break has not yet resolved. 
    public Placement.Type getPlacementType() // Returns whether
```

Para refletir com precisão os anúncios como dicas em uma barra de limpeza, acompanhe o `TimelineEvent`e redesenhe a barra de limpeza toda vez que receber esse evento.

Quando a Resolução de anúncios lenta está ativada para fluxos de VOD, todos os ad breaks são colocados na linha do tempo, no entanto, muitos dos ad breaks ainda não serão resolvidos. O aplicativo pode determinar se esses marcadores devem ser desenhados ou não, verificando o `TimelineMarker::getDuration()`. Se o valor for maior que zero, os anúncios no ad break foram resolvidos.

O TVSDK despacha esse evento quando um ad break é resolvido e também quando o reprodutor passa para o status PREPARADO.

```
mediaPlayer.addEventListener(MediaPlayerEvent.TIMELINE_UPDATED, timelineUpdatedEventListener); 
/** 
* ... 
*/ 
public void onTimelineUpdated(TimelineEvent event) { 
for (PlaybackManagerEventListener listener : eventListeners) { 
  listener.onUpdate(getLocalSeekRange(), event.getTimeline()); 
}
```
