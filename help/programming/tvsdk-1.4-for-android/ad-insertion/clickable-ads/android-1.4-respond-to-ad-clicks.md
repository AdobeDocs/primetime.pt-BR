---
description: Quando um usuário clica em um anúncio ou em um botão relacionado, seu aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.
title: Responder a cliques nos anúncios
exl-id: dc1f1ad7-2f11-4a6c-8459-e02cf8a2e0aa
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 0%

---

# Responder a cliques nos anúncios{#respond-to-clicks-on-ads}

Quando um usuário clica em um anúncio ou em um botão relacionado, seu aplicativo deve responder. O TVSDK fornece informações sobre o URL de destino do clique.

1. Para configurar um ouvinte de eventos para o TVSDK e fornecer as informações de click-through, registre um `AdClickedEventListener.onAdClicked`.

   Quando um usuário clica em um anúncio ou em um botão relacionado, o TVSDK despacha essa notificação, incluindo informações sobre o destino do clique.
1. Monitore as interações do usuário em anúncios clicáveis.
1. Quando o usuário tocar ou clicar no anúncio ou botão, para notificar o TVSDK, chame `notifyClick` no `MediaPlayerView`.
1. Ouça o `onAdClick(AdClickEvent event)` evento do TVSDK.
1. Para recuperar o URL de click-through e informações relacionadas, use os métodos Getter para a variável `AdClickEvent` instância.
1. Pausar o vídeo.

   Para obter mais informações sobre como pausar o vídeo, consulte [Pausar e retomar a reprodução.](../../ad-insertion/clickable-ads/android-1.4-pausing-resuming-playback.md).
1. Use as informações de click-through para exibir o URL de click-through do anúncio e as informações relacionadas.

       Você pode, por exemplo, exibir as informações de uma das seguintes maneiras:
   
   * No aplicativo, abrindo o URL de click-through em um navegador.

      Em plataformas de desktop, a área de reprodução de anúncio de vídeo é usada para chamar URLs de click-through nos cliques do usuário.
   * Redirecione os usuários para seus navegadores web externos para dispositivos móveis.

      Em dispositivos móveis, a área de reprodução de anúncio de vídeo é usada para outras funções, como ocultar e mostrar controles, pausar a reprodução, expandir para tela inteira e assim por diante. Nesses dispositivos, uma exibição separada, como um botão patrocinador, é usada para iniciar o URL de click-through.

1. Feche a janela do navegador na qual as informações de click-through são exibidas e continue a reproduzir o vídeo.

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
