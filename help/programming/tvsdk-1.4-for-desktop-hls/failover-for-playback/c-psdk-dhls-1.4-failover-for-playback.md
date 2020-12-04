---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
seo-description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.
seo-title: Reprodução e failover
title: Reprodução e failover
uuid: 731c087d-9e14-4c7a-a856-c3962b9d7608
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 0%

---


# Visão geral {#playback-and-failover-overview}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. Entretanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como uma interrupção ISP ou uma desconexão de cabo. No entanto, o streaming Primetime oferece proteção contra failover para proteger a reprodução contra determinadas falhas de servidor remoto ou operacionais, o que proporciona uma melhor experiência para os visualizadores. O TVSDK implementa a proteção contra failover para minimizar as interrupções de reprodução e obter uma reprodução contínua, apesar de problemas de transmissão. O player de vídeo muda automaticamente para um conjunto de mídia de backup quando execuções inteiras ou fragmentos não estão disponíveis.
