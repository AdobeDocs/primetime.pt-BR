---
title: Transcodificação just-in-time
description: Transcodificação just-in-time
copied-description: true
exl-id: 9577e1d5-1462-49d6-9d24-94e74dc9c019
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 0%

---

# Transcodificação just-in-time {#just-in-time-transcoding}

O Primetime Ad Insertion apresenta transcodificação e empacotamento just-in-time para garantir que anúncios incompatíveis possam ser reproduzidos corretamente nos fluxos de conteúdo. Ele também pode injetar pacotes ID3 em fragmentos de anúncios que podem ser usados no rastreamento de anúncios do lado do cliente.
Um fluxo de trabalho típico é o seguinte:

1. O Adobe Primetime Ad Insertion busca anúncios/anúncios do servidor de anúncios do cliente.

1. Se o formato criativo de um anúncio for nativamente compatível com o fluxo de conteúdo, o anúncio será inserido no manifesto.

1. Se o formato criativo de um anúncio não for nativamente compatível (por exemplo, .mp4, .mov, .webm), o Primetime Ad Insertion procura uma versão pré-transcodificada do anúncio em um CDN especificado. Se for encontrada, essa publicidade é inserida; caso contrário, o anúncio é enfileirado para transcodificação.

1. Após a transcodificação do anúncio, o Primetime Ad Insertion unirá todas as solicitações subsequentes para esse ativo de anúncio aos manifestos.

O Primetime Ad Insertion suporta transcodificação para a maioria dos formatos de vídeo e linear. A transcodificação criativa de anúncios normalmente ocorre em menos de três minutos. Entre em contato com o representante de suporte do Primetime para obter mais detalhes.
