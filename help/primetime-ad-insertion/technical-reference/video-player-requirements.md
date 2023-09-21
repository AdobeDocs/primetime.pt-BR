---
description: Todos os players de vídeo devem fornecer recursos dos quais o servidor de manifesto depende para inserir anúncios e ativar o rastreamento de anúncios.
title: Requisitos do reprodutor de vídeo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
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
* Os players baseados na Web devem ser executados em plataformas compatíveis com CORS.
