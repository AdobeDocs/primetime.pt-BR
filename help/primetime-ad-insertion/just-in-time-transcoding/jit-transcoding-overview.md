---
title: Transcodificação just-in-time
description: null
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---


# Transcodificação just-in-time {#just-in-time-transcoding}

O Primetime Ad Insertion apresenta transcodificação e empacotamento just-in-time para garantir que anúncios incompatíveis possam ser reproduzidos corretamente nos fluxos de conteúdo. Ele também pode injetar pacotes ID3 em fragmentos de anúncios que podem ser usados no rastreamento de anúncios do cliente.
Um fluxo de trabalho típico é o seguinte:

1. O Adobe Primetime Ad Insertion busca anúncios/anúncios do servidor de anúncios do cliente.

1. Se o formato criativo de um anúncio for nativamente compatível com o fluxo de conteúdo, o anúncio será inserido no manifesto.

1. Se o formato criativo de um anúncio não for nativamente compatível (por exemplo, .mp4, .mov, .webm), o Primetime Ad Insertion pesquisa uma versão pré-transcodificada do anúncio a partir de um CDN especificado. Se for encontrada uma, esta publicidade é inserida; caso contrário, o anúncio será colocado na fila para transcodificação.

1. Depois que o anúncio for transcodificado, o Primetime Ad Insertion unirá todas as solicitações subsequentes desse ativo de anúncio aos manifestos.

O Primetime Ad Insertion suporta transcodificação para a maioria dos formatos de vídeo e linear. A transcodificação criativa de anúncios normalmente ocorre em menos de três minutos. Entre em contato com seu representante de suporte do Primetime para obter mais detalhes.
