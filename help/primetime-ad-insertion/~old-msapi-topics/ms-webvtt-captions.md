---
description: O servidor de manifesto oferece suporte a legendas WebVTT habilitadas para editor para todos os formatos de vídeo HLS. Quando recebe solicitações para inserir anúncios no conteúdo legendado de WebVTT, isso é feito corretamente.
title: Suporte para legendas WebVTT
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Suporte para legendas WebVTT {#support-for-webvtt-captions}

O servidor de manifesto oferece suporte a legendas WebVTT habilitadas para editores para formatos de vídeo HLS/DASH. Quando recebe solicitações para inserir anúncios no conteúdo legendado de WebVTT, isso é feito corretamente.

Se o publicador incluir legendas WebVTT no conteúdo, o servidor de manifesto enviará ao cliente um fluxo de conteúdo com legendas. WebVTT deve ser habilitado pelo publicador para que o servidor de manifesto ofereça suporte a legendas. Quando o cliente tem legendas WebVTT ativadas e envia uma solicitação ao servidor de manifesto, o servidor de manifesto manipula a linha do tempo e o rastreamento de WebVTT e retorna o conteúdo com anúncios e legendas compilados ao cliente.

O fluxo de trabalho para fluxos de conteúdo de VOD é o seguinte:

1. O cliente envia um fluxo de conteúdo com legendas WebVTT habilitadas para o servidor de manifesto.
1. O servidor de manifesto manipula a linha do tempo para compilar anúncios no fluxo de conteúdo.
1. O servidor de manifesto manipula o rastreamento WebVTT para adicionar legendas ao conteúdo (incluindo anúncios).
1. O servidor de manifesto entrega o fluxo de conteúdo ao cliente, com anúncios e legendas inseridos.

>[!NOTE]
>
>Se um segmento de legenda de WebVTT estiver em um anúncio intermediário, o visualizador verá essa legenda ser reproduzida antes e depois desse ad break intermediário. Por exemplo, em um segmento de legenda de 10 segundos com um anúncio intermediário de 30 segundos na marca de 5 segundos, o visualizador vê esse segmento de legenda por 5 segundos antes do intervalo do anúncio intermediário e por 5 segundos após o intermediário.

>[!NOTE]
>
>Se um cliente solicitar que um vídeo seja reproduzido em um idioma específico, como inglês, e, em seguida, solicitar que o vídeo seja reproduzido em francês, o servidor de manifesto não poderá detectar se o cliente solicitou a alteração do idioma para francês. Como o cliente não se comunica com o servidor de manifesto, o servidor de manifesto insere a legenda do anúncio no fluxo de vídeo usando o primeiro idioma especificado no arquivo principal M3U8 do anúncio.
