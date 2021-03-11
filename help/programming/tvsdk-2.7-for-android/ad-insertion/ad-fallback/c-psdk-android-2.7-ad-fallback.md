---
description: Para anúncios VAST (Modelo de veiculação de anúncio de vídeo digital) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
keywords: anúncio de comprimento zero; anúncio vazio
title: Reversão de anúncio para anúncios VAST e VMAP
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---


# Visão geral {#ad-fallback-for-vast-and-vmap-ads-overview}

Para anúncios VAST (Modelo de veiculação de anúncio de vídeo digital) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

A especificação VAST/Digital Video Multiple Ad Playlist (VMAP) declara que, para anúncios com fallback VAST ativado, anúncios vazios acionam automaticamente o uso de anúncios de fallback. Quando um anúncio VAST está vazio, o TVSDK procura uma substituição válida do tipo de mídia HLS entre os anúncios de fallback. Quando um anúncio VAST em um invólucro tem um tipo de mídia inválido, o TVSDK trata esse anúncio como vazio. Você pode configurar se o TVSDK deve fazer o mesmo para anúncios em linha em um VMAP. Para obter mais informações sobre o recurso VAST `fallbackOnNoAd`, consulte [Modelo de veiculação de anúncio de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Anúncios com comprimento zero**  - Quando o TVSDK encontra uma resposta VAST que contém um anúncio de duração zero ou um ad break sem anúncios, ele dispara os eventos AD_BREAK_START / AD_BREAK_COMPLETE para esses anúncios com duração zero. *Esse comportamento se aplica somente a fluxos VOD.* O TVSDK aciona esses eventos mesmo quando o aplicativo está usando a política de anúncios SKIP.
>
>O TVSDK *not* dispara eventos AD_BREAK_START / AD_BREAK_COMPLETE para fluxos Live ou quando um usuário emprega trickplay ou busca passar pelo anúncio de comprimento zero.

