---
description: Você pode ativar ou desativar o recurso Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está desativada por padrão).
keywords: Lazy;Ad resolving;Ad loading;delayLoading
seo-description: Você pode ativar ou desativar o recurso Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está desativada por padrão).
seo-title: Ativar resolução de anúncios ociosos
title: Ativar resolução de anúncios ociosos
uuid: 91884eea-a622-4f5d-b6a8-36bb0050ba1d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b

---


# Ativar resolução de anúncios ociosos {#enable-lazy-ad-resolving}

Você pode ativar ou desativar o recurso Resolução de anúncios preguiçosos usando o mecanismo de Carregamento de anúncios preguiçoso (a Resolução de anúncios preguiçosos está desativada por padrão).

Você pode ativar ou desativar a Resolução de anúncios preguiçosos chamando [AdvertisingMetadata.setDelayLoading](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/com/adobe/mediacore/metadata/AdvertisingMetadata.html#setDelayAdLoading-boolean-) com verdadeiro ou falso.

* Use os métodos Boolean *hasDelayAdLoading* e *setDelayAdLoading* em AdvertisingMetadata para controlar o tempo de resolução do anúncio e o posicionamento dos anúncios na linha do tempo:

   * Se *hasDelayAdLoading* retornar falso, o TVSDK aguarda até que todos os anúncios sejam resolvidos e colocados antes da transição para o estado PREPARADO.
   * Se *hasDelayAdLoading* retornar true, o TVSDK resolve somente os anúncios e transições iniciais para o estado PREPARADO.

      * Os anúncios restantes são resolvidos e colocados durante a reprodução.
   * Quando *hasPreroll *ou *hasLivePreroll* retornar false, o TVSDK assume que não há um anúncio de pré-lançamento e inicia a reprodução do conteúdo imediatamente. Estes são definidos como true.


**APIs relevantes para a resolução de anúncios ociosos:**

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

Para refletir com precisão as publicidades como dicas em uma barra de depuração, escute o `TimelineEvent`evento e redesenhe a barra de depuração sempre que receber esse evento.

Quando a Solução de anúncios ociosos estiver ativada para fluxos VOD, todas as quebras de anúncios serão colocadas na linha do tempo, no entanto, muitas das quebras de anúncios ainda não serão resolvidas. O aplicativo pode determinar se deseja ou não desenhar esses marcadores verificando o `TimelineMarker::getDuration()`. Se o valor for maior que zero, os anúncios no intervalo do anúncio foram resolvidos.

O TVSDK despacha esse evento quando uma pausa de anúncio é resolvida e também quando o player muda para o status PREPARED.

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
