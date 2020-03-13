---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia que é reproduzida localmente.
seo-description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia que é reproduzida localmente.
seo-title: Reprodução e failover
title: Reprodução e failover
uuid: 7bbca3fe-88a3-4384-9a63-eb164c956a75
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Visão geral {#playback-and-failover-overview}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia que é reproduzida localmente.

>[!IMPORTANT]
>
>O Primetime não pode proteger contra falhas como uma interrupção ISP ou uma desconexão de cabo.

O streaming Primetime oferece proteção contra failover para proteger a reprodução contra determinadas falhas de servidor remoto ou falhas operacionais, o que proporciona uma melhor experiência de visualização. Apesar de problemas de transmissão, o TVSDK implementa a proteção contra failover para minimizar as interrupções de reprodução e obter uma reprodução contínua. O player de vídeo muda automaticamente para um conjunto de mídia de backup quando execuções inteiras ou fragmentos não estão disponíveis.