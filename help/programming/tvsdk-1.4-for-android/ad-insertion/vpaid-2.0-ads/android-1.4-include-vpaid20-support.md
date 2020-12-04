---
description: Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
seo-description: Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
seo-title: Implementação da integração com VPAID 2.0
title: Implementação da integração com VPAID 2.0
uuid: 7d11ffd8-240c-4a95-94e6-ff4417c8942e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '65'
ht-degree: 0%

---


# Implementação da integração com VPAID 2.0{#implement-vpaid-integration}

Para adicionar suporte a VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

Para adicionar suporte a VPAID 2.0:

1. Adicione a visualização de anúncio personalizada à interface do player.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Adicione um ouvinte para eventos de anúncio personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

