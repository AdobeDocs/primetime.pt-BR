---
title: Usar Ad Insertion para VOD
description: Uso do Ad Insertion para VOD
translation-type: tm+mt
source-git-commit: 7d74e526dbc4c9f623d1ec30e4bc70d9318a89f9
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 0%

---


# Usar Ad Insertion para VOD {#ad-insertion-vod}

O Primetime Ad Insertion suporta a inserção de anúncios em vários ativos VOD, usando os formatos padrão VAST 3.0+ ou VMAP 1.0+.

* [VMAP IAB](https://www.iab.com/wp-content/uploads/2015/06/VMAPv1_0.pdf)

* [IAB VAST](https://www.iab.com/wp-content/uploads/2015/06/VASTv3_0.pdf)

## VOD (Anúncios mapeados pelo servidor) {#server-mapped-ads}

O Primetime Ad Insertion oferece suporte à inserção de VOD com anúncios inseridos antes do início da reprodução usando informações de linhas do tempo do anúncio definidas em um formato VMAP.  O rastreamento de anúncio específico do VMAP, como os beacons breakStart/breakEnd, será entregue com o Rastreamento [de](set-up-ad-tracking.md)anúncio.

## Reprodução completa de Evento (VOD com paus de Ad Decisioning) {#full-event-replay}

O Primetime Ad Insertion também suporta ativos VOD especializados que contêm dicas no próprio fluxo de conteúdo, como encontrado na reprodução de eventos ao vivo gravados anteriormente. Para obter mais informações sobre os tipos de dicas de decisão de anúncio (ou formatos de sinalização) que suportamos, consulte [Uso do Ad Insertion em tempo real/linear](ad-insertion-live-linear-stream.md).

Oferecemos suporte a cenários de solicitação de anúncio única e de solicitação de anúncio paralela para ativos VOD que contêm mais de uma pausa de anúncio. Para obter mais informações, consulte o `ptmulticall` parâmetro na descrição [](/help/dynamic-ad-insertion/msapi-topics/ms-getting-started/ms-api-query-params.md)Parâmetro. Os formatos VAST e VMAP são suportados para dicas em fluxo.
