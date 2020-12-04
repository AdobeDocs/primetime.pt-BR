---
description: Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.
seo-description: Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.
seo-title: Definir comportamento de anúncio de fallback para anúncios em linha VMAP
title: Definir comportamento de anúncio de fallback para anúncios em linha VMAP
uuid: bc8cb0b4-5ea9-429b-ab5d-746c6f03e74b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Definir comportamento de anúncio de fallback para anúncios em linha VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.

1. Defina `setFallbackOnInvalidCreativeEnabled` como `true` para que o VMAP recue quando o tipo de mídia para um anúncio linear/inline for inválido para HLS.

   O valor padrão é `false`. Se um anúncio linear falhar porque tem um tipo de mídia inválido, ou porque o anúncio não pode ser reempacotado, esse sinalizador permite que o Primetime e a decisão do anúncio sigam o mesmo comportamento de fallback como se o anúncio fosse um invólucro VAST vazio.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
