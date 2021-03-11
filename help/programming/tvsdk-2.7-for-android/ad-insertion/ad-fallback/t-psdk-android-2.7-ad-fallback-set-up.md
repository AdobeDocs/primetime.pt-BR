---
description: Você pode ativar o fallback quando um anúncio em linha do VMAP contiver um tipo de mídia inválido.
title: Definir o comportamento do anúncio de fallback para anúncios em linha do VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---


# Definir o comportamento do anúncio de fallback para anúncios em linha do VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Você pode ativar o fallback quando um anúncio em linha do VMAP contiver um tipo de mídia inválido.

1. Defina `setFallbackOnInvalidCreativeEnabled` como `true` para que o VMAP retorne quando o tipo de mídia para um anúncio linear/em linha for inválido para HLS.

   O valor padrão é `false`. Se um anúncio linear falhar porque tem um tipo de mídia inválido ou porque o anúncio não pode ser reempacotado, esse sinalizador permite que o Primetime e a decisão sigam o mesmo comportamento de fallback que se o anúncio fosse um invólucro VAST vazio.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```

