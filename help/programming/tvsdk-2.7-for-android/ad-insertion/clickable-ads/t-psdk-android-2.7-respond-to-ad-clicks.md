---
description: Quando um usuário clica em um anúncio ou em um botão relacionado, o aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.
title: Responder cliques em anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Responder cliques em anúncios {#respond-to-clicks-on-ads}

O TVSDK fornece informações para que você possa agir com anúncios de click-through. À medida que você cria a interface do usuário do player, deve decidir como responder quando um usuário clica em um anúncio clicável.

Para TVSDK para Android, somente anúncios lineares podem ser clicados.
Quando um usuário clica em um anúncio ou em um botão relacionado, o aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.

1. Para configurar um ouvinte de evento para TVSDK e fornecer as informações de click-through, registre `AdClickedEventListener.onAdClicked`.

   Quando um usuário clica em um anúncio ou em um botão relacionado, o TVSDK envia essa notificação, incluindo informações sobre o destino do clique.
1. Monitore as interações do usuário em anúncios clicáveis.
1. Quando o usuário toca ou clica no anúncio ou botão, para notificar o TVSDK, chame `notifyClick` no `MediaPlayerView`.
1. Analise o evento `onAdClick(AdClickEvent event)` do TVSDK.
1. Para recuperar o URL de click-through e informações relacionadas, use os métodos getter para a instância `AdClickEvent`.
1. Pause o vídeo.

   Para obter mais informações sobre pausar o vídeo, consulte pausing-resume-playback .
1. Use as informações de click-through para exibir o URL de click-through do anúncio e as informações relacionadas.

       Você pode, por exemplo, exibir as informações de uma das seguintes maneiras:
   
   * No seu aplicativo, abrindo o URL de click-through em um navegador.

      Em plataformas de desktop, a área de reprodução do anúncio de vídeo é usada para invocar URLs de click-through nos cliques do usuário.
   * Redirecionar usuários para o navegador da Web móvel externo.

      Em dispositivos móveis, a área de reprodução do anúncio de vídeo é usada para outras funções, como ocultar e mostrar controles, pausar a reprodução, expandir para tela cheia e assim por diante. Nesses dispositivos, uma exibição separada, como um botão patrocinador, é usada para iniciar o URL de click-through.

1. Feche a janela do navegador em que as informações de click-through são exibidas e retome a reprodução do vídeo.

<!--<a id="example_2D93228E510D438C8AB5559897817A47"></a>-->

Por exemplo:

```java
private AdStartedEventListener adStartedEventListener =  
  new AdStartedEventListener() { 
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
 
private AdCompletedEventListener adCompletedEventListener =  
  new AdCompletedEventListener() { 
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
 
private AdClickedEventListener adClickedEventListener =  
  new AdClickedEventListener() { 
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

