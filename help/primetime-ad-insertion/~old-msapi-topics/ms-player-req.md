---
description: Todos os players de vídeo devem fornecer recursos dos quais o servidor de manifesto depende para inserir anúncios e ativar o rastreamento de anúncios.
title: Requisitos do reprodutor de vídeo
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Requisitos do reprodutor de vídeo {#video-player-requirements}

Todos os players de vídeo devem fornecer recursos dos quais o servidor de manifesto depende para inserir anúncios e ativar o rastreamento de anúncios.

Para usar a API de inserção de anúncio do Primetime, um player de vídeo deve atender aos seguintes requisitos:

* Pode rastrear a posição do indicador de reprodução conforme o conteúdo é reproduzido.
* Pode solicitar URLs de rastreamento nos horários especificados.
* É executado em uma plataforma de dispositivo compatível com HLS v3 ou posterior, incluindo:

   * Descontinuidades do PTS marcadas por `EXT-X-DISCONTINUITY` tags
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* É executado em uma plataforma que suporta redirecionamentos HTTP e análise de JSON.
* É executado em uma plataforma compatível com CORS.