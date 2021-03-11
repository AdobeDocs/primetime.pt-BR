---
description: O servidor de manifesto oferece suporte a legendas WebVTT habilitadas pelo editor para todos os formatos de vídeo HLS. Quando recebe solicitações para inserir anúncios no conteúdo legendado da WebVTT, isso ocorre corretamente.
title: Suporte para legendas WebVTT
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Suporte para legendas WebVTT {#support-for-webvtt-captions}

O servidor de manifesto oferece suporte a legendas WebVTT habilitadas pelo editor para formatos de vídeo HLS/DASH. Quando recebe solicitações para inserir anúncios no conteúdo legendado da WebVTT, isso ocorre corretamente.

Se o editor incluir legendas WebVTT no conteúdo, o servidor de manifesto enviará ao cliente um fluxo de conteúdo com legendas. A WebVTT deve ser ativada pelo editor para o servidor de manifesto suportar legendas. Quando o cliente tem legendas WebVTT ativadas e envia uma solicitação ao servidor de manifesto, o servidor de manifesto manipula a linha do tempo e a WebVTT rastreia e retorna o conteúdo com anúncios e legendas compiladas ao cliente.

O fluxo de trabalho para fluxos de conteúdo VOD é o seguinte:

1. O cliente envia um fluxo de conteúdo com legendas WebVTT ativadas para o servidor de manifesto.
1. O servidor de manifesto manipula a linha do tempo para unir anúncios ao fluxo de conteúdo.
1. O servidor manifest manipula o rastreamento WebVTT para adicionar legendas ao conteúdo (incluindo anúncios).
1. O servidor de manifesto fornece o fluxo de conteúdo para o cliente, com anúncios e legendas inseridas.

>[!NOTE]
>
>Se um segmento de legenda da WebVTT estiver em um anúncio intermediário, o visualizador vê essa legenda ser reproduzida antes e depois dessa pausa de anúncio intermediário. Por exemplo, em um segmento de legenda de 10 segundos com um anúncio intermediário de 30 segundos na marca de 5 segundos, o visualizador vê esse segmento de legenda por 5 segundos antes da interrupção do anúncio intermediário e por 5 segundos após a exibição intercalar.

>[!NOTE]
>
>Se um cliente solicitar que um vídeo seja reproduzido em um idioma específico, como o inglês, e, em seguida, solicitar a reprodução do vídeo em francês, o servidor de manifesto não poderá detectar que o cliente solicitou a alteração do idioma para o francês. Como o cliente não se comunica com o servidor de manifesto, o servidor de manifesto insere a legenda do anúncio no fluxo de vídeo usando o primeiro idioma especificado no arquivo principal M3U8 do anúncio.
