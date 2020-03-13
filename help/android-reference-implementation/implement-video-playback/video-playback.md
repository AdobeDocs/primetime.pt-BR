---
seo-title: Operações essenciais da reprodução de vídeo
title: Operações essenciais da reprodução de vídeo
description: O PlaybackManager fornece operações essenciais de streaming de HLS
seo-description: O PlaybackManager fornece operações essenciais de streaming de HLS
uuid: 7ac93f1f-9233-4462-a4be-528d1aa524a9
translation-type: tm+mt
source-git-commit: 31b6cad26bcc393d731080a70eff1c59551f1c8e

---


# Operações essenciais da reprodução de vídeo {#essential-operations-of-video-playback}

O PlaybackManager fornece operações essenciais de streaming HLS:

* Chama o [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), que pode responder adequadamente aos eventos de vídeo.
* Fornece operação de reprodução, como reproduzir, pausar e buscar.
* Retorna as informações sobre o player, como status do player, intervalo de reprodução e fluxo de vídeo ao vivo.
* Determina se o ABR está ativado e define os parâmetros ABR e de controle de buffer dependendo dos dados de configuração fornecidos.
* Determina se o controle de buffer está ativado e define os parâmetros de controle de buffer dependendo dos dados de configuração fornecidos.