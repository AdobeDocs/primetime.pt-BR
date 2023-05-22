---
title: Usar Ad Insertion para VOD
description: Utilização do Ad Insertion para VOD
exl-id: c998938e-f8a6-4ad3-97f6-ca4ad5055f15
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---

# Usar Ad Insertion para VOD {#ad-insertion-vod}

O Primetime Ad Insertion suporta a inserção de anúncios em vários ativos de VOD, usando os formatos padrão VAST 3.0+ ou VMAP 1.0+.

* [IAB VMAP](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (Mapas de anúncios) {#server-mapped-ads}

O Ad Insertion do Primetime suporta a inserção de VOD com anúncios inseridos antes do início da reprodução usando informações de linha do tempo de anúncios definidas em um formato VMAP.  O rastreamento de anúncios específicos do VMAP, como sinais breakStart/breakEnd, será entregue com [Rastreamento de anúncios](set-up-ad-tracking.md).

## Repetição completa de evento (VOD com dicas de Ad Decisioning) {#full-event-replay}

O Primetime Ad Insertion também é compatível com ativos de VOD especializados que contêm dicas no próprio fluxo de conteúdo, como os encontrados na reprodução de eventos ao vivo gravados anteriormente. Para obter mais informações sobre os tipos de dicas de decisão de anúncios (ou formatos cue) compatíveis, consulte [Uso do Ad Insertion no Live/Linear](ad-insertion-live-linear-stream.md).

Oferecemos suporte a cenários de solicitação de anúncios únicos e de solicitação de anúncios múltiplos paralelos para ativos de VOD que contêm mais de um ad break. Para obter mais informações, consulte `ptmulticall` parâmetro em [Descrição do parâmetro](/help/primetime-ad-insertion/technical-reference/bootstrap-api.md). Os formatos VAST e VMAP são compatíveis com dicas em fluxo.
