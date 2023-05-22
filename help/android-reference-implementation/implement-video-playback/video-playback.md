---
title: Operações essenciais de reprodução de vídeo
description: O PlaybackManager fornece operações essenciais de transmissão HLS
exl-id: b4d1b41a-7a16-47f5-be88-6b52f0451813
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
