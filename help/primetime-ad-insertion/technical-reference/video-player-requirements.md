---
description: Todos os players de vídeo devem fornecer recursos dos quais o servidor manifest depende para inserir anúncios e ativar o rastreamento de anúncios.
seo-description: Todos os players de vídeo devem fornecer recursos dos quais o servidor manifest depende para inserir anúncios e ativar o rastreamento de anúncios.
seo-title: Requisitos do player de vídeo
title: Requisitos do player de vídeo
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 0%

---


# Requisitos do player de vídeo {#video-player-requirements}

Todos os players de vídeo devem fornecer recursos dos quais o servidor manifest depende para inserir anúncios e ativar o rastreamento de anúncios.

Para usar a API de inserção de anúncio Primetime, um player de vídeo deve atender ao seguinte:

* É possível rastrear a posição do indicador de reprodução à medida que o conteúdo é reproduzido.
* É possível solicitar URLs de rastreamento nos horários especificados.
* É executado em uma plataforma de dispositivo compatível com HLS v3 ou posterior, incluindo:

   * Descontinuidades do PTS marcadas pelas tags `EXT-X-DISCONTINUITY`
   * `EXT-X-DISCONTINUITY-SEQUENCE`
   * `EXT-X-PROGRAM-DATE-TIME`
   * `EXT-X-START`

* É executado em uma plataforma que suporta redirecionamentos HTTP e análise JSON.
* Os players baseados na Web devem ser executados em plataformas compatíveis com CORS.