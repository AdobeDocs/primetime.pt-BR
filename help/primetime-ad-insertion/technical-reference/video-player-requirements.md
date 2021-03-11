---
description: Todos os players de vídeo devem fornecer recursos dos quais o servidor de manifesto depende para inserir anúncios e ativar o rastreamento de anúncios.
title: Requisitos do reprodutor de vídeo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Requisitos do reprodutor de vídeo {#video-player-requirements}

Todos os players de vídeo devem fornecer recursos dos quais o servidor de manifesto depende para inserir anúncios e ativar o rastreamento de anúncios.

Para usar a API de inserção de anúncio do Primetime, um reprodutor de vídeo deve atender ao seguinte:

* Pode rastrear a posição do indicador de reprodução à medida que o conteúdo é reproduzido.
* Pode solicitar URLs de rastreamento nos horários especificados.
* É executado em uma plataforma de dispositivo compatível com HLS v3 ou posterior, incluindo:

   * Descontinuações de PTS marcadas pelas tags `EXT-X-DISCONTINUITY`
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* É executado em uma plataforma que oferece suporte a redirecionamentos HTTP e à análise JSON.
* Os players baseados na Web devem ser executados em plataformas compatíveis com CORS.