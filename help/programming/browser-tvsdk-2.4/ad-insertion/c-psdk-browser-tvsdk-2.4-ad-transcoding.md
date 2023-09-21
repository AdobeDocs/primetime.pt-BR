---
description: Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming sobre HTTP (DASH) porque seu formato de vídeo é incompatível com HLS/DASH. A inserção de anúncios no Adobe Primetime e o TVSDK do navegador podem, opcionalmente, tentar reempacotar (transcodificar) vídeos incompatíveis em vídeos m3u8/mpd compatíveis.
title: Reempacotar (transcodificar) anúncios incompatíveis
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 0%

---

# Reempacotar (transcodificar) anúncios incompatíveis{#repackage-transcode-incompatible-ads}

Alguns anúncios de terceiros (ou criativos) não podem ser compilados no fluxo de conteúdo HTTP Live Streaming (HLS)/Dynamic Adaptive Streaming sobre HTTP (DASH) porque seu formato de vídeo é incompatível com HLS/DASH. A inserção de anúncios no Adobe Primetime e o TVSDK do navegador podem, opcionalmente, tentar reempacotar (transcodificar) vídeos incompatíveis em vídeos m3u8/mpd compatíveis.

Anúncios veiculados por vários terceiros, como um servidor de publicidade de uma agência, um parceiro de inventário ou uma rede de publicidade, geralmente são entregues em formatos incompatíveis, como o MP4 de download progressivo.
