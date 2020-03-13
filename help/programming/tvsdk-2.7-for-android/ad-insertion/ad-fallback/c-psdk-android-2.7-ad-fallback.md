---
description: Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
keywords: zero length ad;empty ad
seo-description: Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
seo-title: Anúncio de fallback para anúncios VAST e VMAP
title: Anúncio de fallback para anúncios VAST e VMAP
uuid: ecfeff31-b723-4a0d-99f2-48705a37b5f0
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Visão geral {#ad-fallback-for-vast-and-vmap-ads-overview}

Para anúncios (ou anúncios) do Modelo de disponibilização de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

A especificação VAST/Digital Video Multiple Ad Playlist (VMAP) declara que para anúncios com fallback VAST ativado, anúncios vazios acionam automaticamente o uso de anúncios fallback. Quando um anúncio VAST está vazio, o TVSDK procura uma substituição válida do tipo de mídia HLS entre os anúncios de fallback. Quando um anúncio VAST em um invólucro tem um tipo de mídia inválido, o TVSDK trata esse anúncio como vazio. Você pode configurar se o TVSDK deve fazer o mesmo para anúncios em linha em um VMAP. Para obter mais informações sobre o `fallbackOnNoAd` recurso VAST, consulte Modelo de disponibilização de vídeo [digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Anúncios** de tamanho zero - quando o TVSDK encontra uma resposta VAST que contém um anúncio de duração zero ou uma pausa de anúncio sem anúncios, ele aciona os eventos AD_BREAK_START / AD_BREAK_COMPLETE para essas pausas de anúncio de comprimento zero. *Esse comportamento se aplica somente a fluxos VOD.* O TVSDK aciona esses eventos mesmo quando seu aplicativo está usando a política de anúncios SKIP.
>
>O TVSDK *não* dispara eventos AD_BREAK_START / AD_BREAK_COMPLETE para fluxos ao vivo, ou quando um usuário usa trickplay ou procura passar do anúncio de comprimento zero.

