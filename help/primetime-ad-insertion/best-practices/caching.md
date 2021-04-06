---
title: Armazenamento em cache
description: Armazenamento em cache
copied-description: true
exl-id: c12c2345-db55-468a-b4b5-5a9e1364a46d
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Cache HTTP {#caching}

O Primetime Ad Insertion por padrão respeita os cabeçalhos de controle de cache HTTP ao buscar anúncios e também conteúdo.  Isso pode reduzir drasticamente a quantidade de solicitações de rede necessárias para o Primetime Ad Insertion para fazer a CDN em todos os clientes.  Para armazenamento em cache, o Adobe recomenda as seguintes configurações e envolve o envio do cabeçalho HTTP `max-age` do CDN.  Entre em contato com seu representante de CDN para ativar esses cabeçalhos nos fluxos de vídeo e anúncios.

## Para conteúdo Live/Linear {#caching-live-linear-content}

* Manifesto principal: 24 horas ou Controle de Cache: max-age=86400
* Manifesto de mídia: 1 segundo ou Controle de Cache: max-age=1

## Para conteúdo VOD {#caching-vod-content}

* Manifesto principal: 24 horas ou Controle de Cache: max-age=86400
* Manifesto de mídia: 24 horas ou Controle de Cache: max-age=86400
