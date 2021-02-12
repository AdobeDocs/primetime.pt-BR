---
description: O servidor manifest suporta legendas WebVTT habilitadas pelo editor para todos os formatos de vídeo HLS. Quando recebe solicitações para inserir publicidades no conteúdo legendado WebVTT, isso ocorre corretamente.
seo-description: O servidor manifest suporta legendas WebVTT habilitadas pelo editor para todos os formatos de vídeo HLS/DASH. Quando recebe solicitações para inserir publicidades no conteúdo legendado WebVTT, isso ocorre corretamente.
seo-title: Suporte para legendas WebVTT
title: Suporte para legendas WebVTT
uuid: 1dc728b0-5aeb-4c48-8f3b-54ff4b135742
translation-type: tm+mt
source-git-commit: e437f4143fb939f46d106c64efc391137c33fe17
workflow-type: tm+mt
source-wordcount: '357'
ht-degree: 0%

---


# Suporte para legendas WebVTT {#support-for-webvtt-captions}

O servidor manifest suporta legendas WebVTT habilitadas pelo editor para formatos de vídeo HLS/DASH. Quando recebe solicitações para inserir publicidades no conteúdo legendado WebVTT, isso ocorre corretamente.

Se o editor incluir legendas WebVTT no conteúdo, o servidor manifest enviará ao cliente um fluxo de conteúdo com legendas. A WebVTT deve ser ativada pelo editor do servidor manifest para suportar legendas. Quando o cliente tem legendas WebVTT ativadas e envia uma solicitação para o servidor manifest, o servidor manifest manipula a linha do tempo e o rastreamento WebVTT e retorna o conteúdo com anúncios e legendas agrupadas ao cliente.

O fluxo de trabalho para fluxos de conteúdo VOD é o seguinte:

1. O cliente envia um fluxo de conteúdo com legendas WebVTT ativadas para o servidor de manifesto.
1. O servidor manifest manipula a linha do tempo para unir publicidades ao fluxo de conteúdo.
1. O servidor manifest manipula o rastreamento WebVTT para adicionar legendas ao conteúdo (incluindo anúncios).
1. O servidor manifest fornece o fluxo de conteúdo para o cliente, com anúncios e legendas inseridas.

>[!NOTE]
>
>Se um segmento de legenda WebVTT estiver dentro de um anúncio intermediário, o visualizador verá essa legenda ser reproduzida antes e depois dessa pausa intermediária do anúncio. Por exemplo, em um segmento de legenda de 10 segundos com um anúncio intermediário de 30 segundos na marca de 5 segundos, o visualizador visualiza esse segmento de legenda por 5 segundos antes do intervalo intermediário do anúncio e por 5 segundos após o mid-roll.

>[!NOTE]
>
>Se um cliente solicitar que um vídeo seja reproduzido em um idioma específico, como inglês, e solicitar que o vídeo seja reproduzido em francês, o servidor manifest não poderá detectar que o cliente solicitou a alteração do idioma para francês. Como o cliente não se comunica com o servidor manifest, o servidor manifest insere a legenda do anúncio no fluxo de vídeo usando o primeiro idioma especificado no arquivo principal M3U8 do anúncio.
