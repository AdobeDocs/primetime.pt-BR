---
title: Armazenamento em cache
description: Armazenamento em cache
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# Cache de HTTP {#caching}

Por padrão, o Primetime Ad Insertion respeita os cabeçalhos de controle de cache HTTP ao buscar anúncios criativos, bem como conteúdo.  Isso pode reduzir bastante a quantidade de solicitações de rede necessárias para o Ad Insertion do Primetime fazer à CDN em todos os clientes.  Para armazenamento em cache, o Adobe recomenda as seguintes configurações e envolve o envio do cabeçalho HTTP `max-age` do CDN.  Entre em contato com o representante da CDN para ativar esses cabeçalhos nos fluxos de vídeo e fluxos de anúncios.

## Para conteúdo Live/Linear {#caching-live-linear-content}

* Manifesto principal: 24 horas ou Cache-Control: max-age=86400
* Manifesto de mídia: 1 segundo ou Cache-Control: max-age=1

## Para conteúdo de VOD {#caching-vod-content}

* Manifesto principal: 24 horas ou Cache-Control: max-age=86400
* Manifesto de mídia: 24 horas ou Cache-Control: max-age=86400
