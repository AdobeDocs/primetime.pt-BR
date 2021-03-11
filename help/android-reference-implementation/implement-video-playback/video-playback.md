---
title: Operações essenciais de reprodução de vídeo
description: O PlaybackManager fornece operações essenciais de transmissão de HLS
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Operações essenciais de reprodução de vídeo {#essential-operations-of-video-playback}

O PlaybackManager fornece operações essenciais de transmissão de HLS:

* Chama o [PlaybackManagerEventListener](https://help.adobe.com/en_US/primetime/api/reference_implementation/android/javadoc/com/adobe/primetime/reference/manager/PlaybackManager.PlaybackManagerEventListener.html), que pode responder adequadamente a eventos de vídeo.
* Fornece a operação de reprodução, como reprodução, pausa e busca.
* Retorna as informações sobre o reprodutor, como o status do reprodutor, o intervalo de reprodução e o fluxo de vídeo ao vivo.
* Determina se o ABR está ativado e define os parâmetros ABR e de controle de buffer dependendo dos dados de configuração fornecidos.
* Determina se o controle de buffer está ativado e define os parâmetros de controle de buffer dependendo dos dados de configuração fornecidos.