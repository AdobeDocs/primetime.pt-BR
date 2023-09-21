---
title: Operações essenciais de reprodução de vídeo
description: O PlaybackManager fornece operações essenciais de transmissão HLS
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---

# Operações essenciais de reprodução de vídeo {#essential-operations-of-video-playback}

O PlaybackManager fornece operações essenciais de transmissão HLS:

* Chama o [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), que podem responder adequadamente a eventos de vídeo.
* Fornece a operação de reprodução, como reproduzir, pausar e buscar.
* Retorna as informações sobre o player, como status do player, intervalo de reprodução e transmissão de vídeo ao vivo.
* Determina se o ABR está ativado e define os parâmetros de controle do ABR e do buffer, dependendo dos dados de configuração fornecidos.
* Determina se o controle de buffer está ativado e define os parâmetros de controle de buffer dependendo dos dados de configuração fornecidos.
