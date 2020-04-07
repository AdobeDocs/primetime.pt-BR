---
description: Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
seo-description: Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
seo-title: Implementação da integração com VPAID 2.0
title: Implementação da integração com VPAID 2.0
uuid: fa5b9cdd-e684-4656-91b7-50781dc59e23
translation-type: tm+mt
source-git-commit: 25f97c8d296f71deddc8f9d12b97007ddf73f603

---


# Implementação da integração com VPAID 2.0 {#implement-vpaid-integration}

Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

Para adicionar suporte a VPAID 2.0:

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

1. Crie ouvintes e processe os eventos descritos em ouvintes de eventos.

   >[!IMPORTANT]
   >
   >Em um fluxo de trabalho VPAID 2.0, para visualizações de anúncio personalizadas, é muito importante manter sua `CustomAdView` instância entre `AdBreak` start (evento `AD_BREAK_START`) e `AdBreak` conclusões (evento `AD_BREAK_COMPLETE`), do momento em que você cria a visualização de anúncio personalizada até quando ela é descartada. Ou seja, não crie uma visualização de anúncio personalizada em cada start de intervalo de anúncios e descarte-a em cada intervalo de anúncios concluído.
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
   >```
   >
   >Finalmente, antes de descartar sua visualização de anúncio personalizada, você deve removê-la do `FrameLayout`. Por exemplo:
   >
   >
   ```
   >if (_playerFrame != null) 
   >       _playerFrame.removeAllViews(); 
   >```
