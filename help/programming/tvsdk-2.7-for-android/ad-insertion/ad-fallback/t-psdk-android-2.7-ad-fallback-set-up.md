---
description: Você pode habilitar o fallback quando um anúncio em linha do VMAP contiver um tipo de mídia inválido.
title: Definir comportamento de anúncio de fallback para anúncios em linha do VMAP
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 0%

---

# Definir comportamento de anúncio de fallback para anúncios em linha do VMAP {#define-fallback-ad-behavior-for-vmap-inline-ads}

Você pode habilitar o fallback quando um anúncio em linha do VMAP contiver um tipo de mídia inválido.

1. Definir `setFallbackOnInvalidCreativeEnabled` para `true` para que o VMAP retorne quando o tipo de mídia de um anúncio linear/em linha for inválido para HLS.

   O valor padrão é `false`. Se um anúncio linear falhar porque tem um tipo de mídia inválido ou porque o anúncio não pode ser reempacotado, esse sinalizador permitirá que as decisões de anúncios do Primetime sigam o mesmo comportamento de fallback que um anúncio VAST vazio.

   ```java
   AuditudeSettings result = new AuditudeSettings(); 
   result.setFallbackOnInvalidCreative(true);
   ```
