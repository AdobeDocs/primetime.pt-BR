---
description: Quando um usuário clica em um anúncio ou botão relacionado, seu aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.
seo-description: Quando um usuário clica em um anúncio ou botão relacionado, seu aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.
seo-title: Responder a cliques em anúncios
title: Responder a cliques em anúncios
uuid: 31852f01-c900-48e3-ae23-7fb131c22594
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Responder a cliques em anúncios{#respond-to-clicks-on-ads}

Quando um usuário clica em um anúncio ou botão relacionado, seu aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.

1. Para configurar um ouvinte de evento para TVSDK e fornecer as informações de click-through, registre e e `AdClickedEventListener.onAdClicked`.

   Quando um usuário clica em um anúncio ou botão relacionado, o TVSDK envia essa notificação, incluindo informações sobre o destino do clique.
1. Monitore as interações do usuário em anúncios clicáveis.
1. Quando o usuário toca ou clica no anúncio ou botão, para notificar o TVSDK, chama `notifyClick` o `MediaPlayerView`.
1. Analise o `onAdClick(AdClickEvent event)` evento do TVSDK.
1. Para recuperar o URL de click-through e as informações relacionadas, use os métodos getter para a `AdClickEvent` instância.
1. Pause o vídeo.

   Para obter mais informações sobre como pausar o vídeo, consulte [Pausar e retomar a reprodução.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. Use as informações de click-through para exibir o URL de click-through do anúncio e as informações relacionadas.

       Você pode, por exemplo, exibir as informações de uma das seguintes maneiras:
   
   * Em seu aplicativo, abrindo o URL de click-through em um navegador.

      Em plataformas de desktop, a área de reprodução de vídeo e anúncio é usada para invocar URLs de click-through nos cliques do usuário.
   * Redirecione os usuários para seu navegador móvel externo.

      Em dispositivos móveis, a área de reprodução do anúncio de vídeo é usada para outras funções, como ocultar e mostrar controles, pausar a reprodução, expandir para tela cheia e assim por diante. Nesses dispositivos, uma exibição separada, como um botão patrocinador, é usada para iniciar o URL de click-through.

1. Feche a janela do navegador na qual as informações de click-through são exibidas e retome a reprodução do vídeo.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

Por exemplo:

```java
private AdStartedEventListener adStartedEventListener = new AdStartedEventListener() { 
    @Override 
    public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        if (ad == null) { 
            return; 
        } 
 
        _pubOverlay.startAd(adPlaybackEvent.getAdBreak(), ad); 
 
        if (areClickableAdsEnabled() && ad.isClickable()) { 
            _isClickableAdPlaying = true; 
            _playerClickableAdFragment.show(); 
        } 
 
    } 
}; 
 
private AdCompletedEventListener adCompletedEventListener = new AdCompletedEventListener() { 
    @Override 
    public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { 
        Ad ad = adPlaybackEvent.getAd(); 
        _pubOverlay.stopAd(adPlaybackEvent.getAdBreak(), ad); 
 
        _isClickableAdPlaying = false; 
        if (ad.isClickable()) { 
            _playerClickableAdFragment.hide(); 
        } 
    } 
}; 
 
private AdClickedEventListener adClickedEventListener = new AdClickedEventListener() { 
    @Override 
    public void onAdClicked(AdClickEvent adClickEvent) { 
        AdClick adClick = adClickEvent.getAdClick(); 
        Ad ad = adClickEvent.getAd(); 
 
        String url = adClick.getUrl(); 
        if (url == null || url.trim().equals("")) { 
        } else { 
            Uri uri = Uri.parse(url); 
            Intent intent = new Intent(ACTION_VIEW, uri); 
            try { 
                startActivity(intent); 
            } catch (Exception e) { 
            } 
        } 
 
    } 
}; 
```

