---
title: Cache
description: null
translation-type: tm+mt
source-git-commit: 76dc54fabdae400ad708ba83fcf6f7fd5caa2b22
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 0%

---


# Cache HTTP {#caching}

Por padrão, o Primetime Ad Insertion respeita os cabeçalhos de controle do cache HTTP ao buscar anúncios e anúncios, bem como o conteúdo.  Isso pode reduzir drasticamente a quantidade de solicitações de rede necessárias para o Primetime Ad Insertion para fazer o CDN em todos os clientes.  Para armazenamento em cache, o Adobe recomenda as seguintes configurações e envolve o envio do cabeçalho HTTP `max-age` do CDN.  Entre em contato com seu representante de CDN para ativar esses cabeçalhos nos streams de vídeo e anúncios.

## Para conteúdo ao vivo/linear {#caching-live-linear-content}

* Manifesto principal: 24 horas ou controle de cache: max-age=86400
* Manifesto de mídia: 1 segundo ou Controle de cache: max-age=1

## Para conteúdo VOD {#caching-vod-content}

* Manifesto principal: 24 horas ou controle de cache: max-age=86400
* Manifesto de mídia: 24 horas ou controle de cache: max-age=86400
