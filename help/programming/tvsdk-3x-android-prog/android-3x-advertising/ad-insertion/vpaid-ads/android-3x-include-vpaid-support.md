---
description: Para adicionar suporte a VPAID 2.0, adicione uma exibição de anúncio personalizada e ouvintes apropriados.
seo-description: Para adicionar suporte a VPAID 2.0, adicione uma exibição de anúncio personalizada e ouvintes apropriados.
seo-title: Implementação da integração com VPAID 2.0
title: Implementação da integração com VPAID 2.0
uuid: d512fb5b-001c-4a7a-a553-d5962002bb30
translation-type: tm+mt
source-git-commit: 1034a0520590777cc0930d2f732741202bc3bc04

---


# Implementação da integração com VPAID 2.0 {#implement-vpaid-integration}

Para adicionar suporte a VPAID 2.0, adicione uma exibição de anúncio personalizada e ouvintes apropriados.

1. Adicione a exibição de anúncio personalizada à interface do player quando o player estiver no estado PREPARADO.

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
   >Em um fluxo de trabalho do VPAID 2.0, para exibições de anúncios personalizadas, é muito importante manter sua `CustomAdView` instância durante `AdBreak` inicializações (evento `AD_BREAK_START`) e `AdBreak` conclusões (evento `AD_BREAK_COMPLETE`), do momento em que você cria a exibição de anúncio personalizada até quando ela é descartada. Ou seja, não crie uma exibição de anúncio personalizada em cada início de quebra de anúncio e descarte-a em cada conclusão de quebra de anúncio.
   >
   >
   >Além disso, você só deve criar sua exibição de anúncio personalizada quando o player estiver no estado PREPARADO,
   >
   >
   >Descarte somente a exibição de anúncio personalizada quando redefinir for chamado. Por exemplo:    >
   >
   >
   ```>
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >
   >```

   Finalmente, antes de descartar sua exibição de anúncio personalizada, você deve removê-la do `FrameLayout`. Por exemplo:
   >```
   >if (_playerFrame != null) 
      _playerFrame.removeAllViews(); 
   ```
