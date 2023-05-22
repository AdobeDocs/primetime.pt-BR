---
description: Para anúncios (ou criações) do Modelo de veiculação de anúncios de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.
keywords: anúncio de comprimento zero;anúncio vazio
title: Fallback de anúncios para anúncios VAST e VMAP
exl-id: 1fc04cac-e83f-4c1f-bf7b-1cbcb2135d53
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 0%

---

# Visão geral {#ad-fallback-for-vast-and-vmap-ads-overview}

Para anúncios (ou criações) do Modelo de veiculação de anúncios de vídeo digital (VAST) com a regra de fallback ativada, o TVSDK trata um anúncio com um tipo de mídia inválido como um anúncio vazio e tenta usar anúncios de fallback em seu lugar. Você pode configurar alguns aspectos do comportamento de fallback.

A especificação VAST/Digital Video Multiple Ad Playlist (VMAP) informa que, para anúncios com o recurso de fallback VAST ativado, anúncios vazios acionam automaticamente o uso de anúncios de fallback. Quando um anúncio VAST está vazio, o TVSDK procura uma substituição de tipo de mídia HLS válida entre os anúncios de fallback. Quando um anúncio VAST em um invólucro tem um tipo de mídia inválido, o TVSDK trata esse anúncio como vazio. Você pode configurar se o TVSDK deve fazer o mesmo para anúncios em linha em um VMAP. Para obter mais informações sobre o VAST `fallbackOnNoAd` recurso, consulte [Modelo de veiculação de anúncio de vídeo digital (VAST) 3.0](https://www.iab.net/guidelines/508676/digitalvideo/vsuite/vast).

>[!NOTE]
>
>**Anúncios com comprimento zero** - Quando o TVSDK encontra uma resposta VAST que contém um anúncio de duração zero ou um ad break sem anúncios, ele aciona eventos AD_BREAK_START / AD_BREAK_COMPLETE para esses ad breaks de duração zero. *Esse comportamento se aplica somente a fluxos de VOD.* O TVSDK aciona esses eventos mesmo quando o aplicativo está usando a política IGNORAR anúncio.
>
>O TVSDK faz *não* acione os eventos AD_BREAK_START / AD_BREAK_COMPLETE para transmissões em tempo real ou quando um usuário emprega a reprodução artificial ou busca ultrapassar o anúncio de comprimento zero.
