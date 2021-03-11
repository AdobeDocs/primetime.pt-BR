---
description: Para adicionar suporte ao VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.
title: Implementar a integração com o VPAID 2.0
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '50'
ht-degree: 0%

---


# Implementar a integração do VPAID 2.0{#implement-vpaid-integration}

Para adicionar suporte ao VPAID 2.0, adicione uma visualização de anúncio personalizada e ouvintes apropriados.

Para adicionar suporte ao VPAID 2.0:

1. Adicione a visualização de anúncio personalizada à interface do reprodutor.

   ```java
   _playerFrame.addView(mediaPlayer.createCustomAdView());
   ```

1. Adicione um ouvinte para eventos de anúncio personalizados.

   ```java
   mediaplayer.addEventListener(MediaPlayer.Event.CUSTOM_AD,  
     _customAdEventListener);
   ```

