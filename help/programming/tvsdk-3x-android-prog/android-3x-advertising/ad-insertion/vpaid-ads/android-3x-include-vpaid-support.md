---
description: Para adicionar suporte ao VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
title: Implementar a integração com o VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 2%

---


# Implementar a integração do VPAID 2.0 {#implement-vpaid-integration}

Para adicionar suporte ao VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

1. Adicione a visualização de anúncio personalizada à interface do reprodutor quando ele estiver no estado PREPARADO.

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

1. Crie ouvintes e processe os eventos descritos em [Events](../../../../tvsdk-3x-android-prog/android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   >[!IMPORTANT]
   >
   >Em um fluxo de trabalho VPAID 2.0, para exibições de anúncios personalizadas, é muito importante manter sua instância `CustomAdView` em `AdBreak` inícios (evento `AD_BREAK_START`) e `AdBreak` conclusões (evento `AD_BREAK_COMPLETE`), do momento em que você cria a exibição de anúncio personalizada até quando ela é eliminada. Ou seja, não crie uma visualização de anúncio personalizada em cada início e descarte-a em cada conclusão de ad break.
   >
   >
   >Além disso, você só deve criar sua visualização de anúncio personalizada quando o player estiver no estado PREPARADO,
   >
   >
   >Descarte apenas a exibição de anúncio personalizada quando a redefinição for chamada. Por exemplo:
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
