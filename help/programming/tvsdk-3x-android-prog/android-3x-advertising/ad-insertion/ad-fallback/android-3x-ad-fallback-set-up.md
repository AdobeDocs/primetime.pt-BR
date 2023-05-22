---
description: Você pode habilitar o fallback quando um anúncio em linha do VMAP contiver um tipo de mídia inválido.
title: Definir comportamento de anúncio de fallback para anúncios em linha do VMAP
exl-id: 50de85b0-df2b-422f-893c-dfa641b4901e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
