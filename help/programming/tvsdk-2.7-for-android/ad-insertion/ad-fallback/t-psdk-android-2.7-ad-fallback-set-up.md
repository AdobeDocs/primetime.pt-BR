---
description: Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.
seo-description: Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.
seo-title: Definir comportamento de anúncio de fallback para anúncios em linha VMAP
title: Definir comportamento de anúncio de fallback para anúncios em linha VMAP
uuid: a7b5c9a6-f546-4d3a-9d49-7e5484acff7a
translation-type: tm+mt
source-git-commit: 812d04037c3b18f8d8cdd0d18430c686c3eee1ff

---


# Definir comportamento de anúncio de fallback para anúncios em linha VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Você pode ativar o fallback quando um anúncio em linha VMAP contiver um tipo de mídia inválido.

1. Defina `setFallbackOnInvalidCreativeEnabled` para que `true` o VMAP volte quando o tipo de mídia para um anúncio linear/inline for inválido para HLS.

   O valor padrão é `false`. Se um anúncio linear falhar porque tem um tipo de mídia inválido, ou porque o anúncio não pode ser reempacotado, esse sinalizador permite que o Primetime e a decisão do anúncio sigam o mesmo comportamento de fallback como se o anúncio fosse um invólucro VAST vazio.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

