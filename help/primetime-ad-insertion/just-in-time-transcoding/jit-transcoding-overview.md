---
title: Transcodificação Just-in-Time
description: Transcodificação Just-in-Time
copied-description: true
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Transcodificação Just-in-Time {#just-in-time-transcoding}

O Primetime Ad Insertion apresenta empacotamento e transcodificação just-in-time para garantir que anúncios incompatíveis possam ser reproduzidos corretamente em fluxos de conteúdo. Ele também pode injetar pacotes de ID3 em fragmentos de anúncios que podem ser usados no rastreamento de anúncios do lado do cliente.
Um fluxo de trabalho típico é o seguinte:

1. O Adobe Primetime Ad Insertion busca anúncios/criações no servidor de anúncios do cliente.

1. Se o formato criativo de um anúncio for nativamente compatível com o fluxo de conteúdo, o criativo será inserido no manifesto.

1. Se o formato criativo de um anúncio não for nativamente compatível (por exemplo, .mp4, .mov, .webm), o Primetime Ad Insertion procurará uma versão pré-transcodificada do anúncio em um CDN especificado. Se um for encontrado, esse anúncio será inserido; caso contrário, o anúncio será enfileirado para transcodificação.

1. Depois que o criativo do anúncio for transcodificado, o Primetime Ad Insertion unirá todas as solicitações subsequentes desse ativo de anúncio nos manifestos.

O Ad Insertion do Primetime suporta transcodificação para a maioria dos formatos de vídeo e lineares. A transcodificação criativa de anúncios normalmente ocorre em menos de três minutos. Entre em contato com o representante de suporte do Primetime para obter mais detalhes.
