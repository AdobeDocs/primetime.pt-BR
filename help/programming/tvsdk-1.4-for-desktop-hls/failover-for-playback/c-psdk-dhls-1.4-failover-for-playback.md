---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão de Internet de um visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
title: Reprodução e failover
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---


# Visão geral {#playback-and-failover-overview}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão de Internet de um visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como uma interrupção de ISP ou uma desconexão de cabo. No entanto, o streaming do Primetime oferece proteção contra failover para proteger a reprodução de determinadas falhas de servidor remoto ou falhas operacionais, o que melhora a experiência dos visualizadores. O TVSDK implementa a proteção contra failover para minimizar as interrupções da reprodução e obter uma reprodução contínua apesar dos problemas de transmissão. O reprodutor de vídeo muda automaticamente para um conjunto de mídia de backup quando representações inteiras ou fragmentos não estão disponíveis.
