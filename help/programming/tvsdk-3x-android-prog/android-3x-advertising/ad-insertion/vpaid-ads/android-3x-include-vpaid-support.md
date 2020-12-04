---
description: Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
seo-description: Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
seo-title: Implementação da integração com VPAID 2.0
title: Implementação da integração com VPAID 2.0
uuid: d512fb5b-001c-4a7a-a553-d5962002bb30
translation-type: tm+mt
source-git-commit: 83df68905f74931355264661aed6cff43b802d3f
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 2%

---


# Implementação da integração com VPAID 2.0 {#implement-vpaid-integration}

Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

1. Adicione a visualização de anúncio personalizada à interface do player quando o player estiver no estado PREPARADO.

   ```java
   ... 
   private FrameLayout _playerFrame; 
       ... 
       case PREPARED: 
           ... 
           addCustomView(); 
   ... 
   private void addCustomView() { 
       ... 
       WebView view = (WebView)_mediaPlayer.getCustomAdView(); 
       ... 
       _playerFrame.addView(view);
   ```

1. Crie ouvintes e processe os eventos descritos em [Eventos](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >Em um fluxo de trabalho VPAID 2.0, para visualizações de anúncio personalizadas, é muito importante manter sua instância `CustomAdView` em start `AdBreak` (evento `AD_BREAK_START`) e `AdBreak` em conclusões (evento `AD_BREAK_COMPLETE`), desde o momento em que você cria a visualização de anúncio personalizada até quando ela é descartada. Ou seja, não crie uma visualização de anúncio personalizada em cada start de intervalo de anúncios e descarte-a em cada intervalo de anúncios concluído.
   >
   >
   >Além disso, você só deve criar sua visualização de anúncio personalizada quando o player estiver no estado PREPARADO,
   >
   >
   >Descarte somente a visualização de anúncio personalizada quando redefinir for chamado. Por exemplo:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```
   >
   >Finalmente, antes de descartar sua visualização de anúncio personalizada, você deve removê-la do `FrameLayout`. Por exemplo:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
