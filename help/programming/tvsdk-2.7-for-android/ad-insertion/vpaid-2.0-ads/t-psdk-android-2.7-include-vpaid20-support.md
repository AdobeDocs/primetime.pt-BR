---
description: Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
title: Implementar a integração com VPAID 2.0
exl-id: 8a6b81e7-1034-48fc-87aa-4cb8ab305d15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 0%

---

# Implementar a integração com VPAID 2.0 {#implement-vpaid-integration}

Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

Para adicionar suporte a VPAID 2.0:

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

1. Crie ouvintes e processe os eventos descritos em ouvintes de eventos.

   >[!IMPORTANT]
   >
   >Em um fluxo de trabalho VPAID 2.0, para exibições de anúncios personalizadas, é muito importante manter `CustomAdView` instância através `AdBreak` inicia (evento) `AD_BREAK_START`) e `AdBreak` conclui (evento `AD_BREAK_COMPLETE`), desde o momento em que você cria a visualização de anúncio personalizada até o momento em que você a descarta. Ou seja, não crie uma visualização de anúncio personalizada em cada início de ad break e descarte-a em cada conclusão de ad break.
   >
   >
   >Além disso, você só deve criar a visualização de anúncio personalizada quando o reprodutor estiver no estado PREPARADO,
   >
   >
   >Descartar apenas a exibição de anúncio personalizada quando a redefinição for chamada. Por exemplo:
   >
   >
   ```
   >// on reset 
   >if (_mediaPlayer != null) { 
   >       _mediaPlayer.disposeCustomAdView(); 
   >       ... 
   >} 
   >```
   >
   >Finalmente, antes de descartar sua visualização de anúncio personalizada, você deve removê-la da `FrameLayout`. Por exemplo:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
