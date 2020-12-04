---
description: Todos os players de vídeo devem fornecer recursos dos quais o servidor manifest depende para inserir anúncios e ativar o rastreamento de anúncios.
seo-description: Todos os players de vídeo devem fornecer recursos dos quais o servidor manifest depende para inserir anúncios e ativar o rastreamento de anúncios.
seo-title: Requisitos do player de vídeo
title: Requisitos do player de vídeo
uuid: 29593d67-2901-4d9e-a08f-23c8a7667283
translation-type: tm+mt
source-git-commit: 358c5b02d47f23a6adbc98e457e56c8220cae6e9
workflow-type: tm+mt
source-wordcount: '136'
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
* É executado em uma plataforma compatível com CORS.