---
description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia que é reproduzida localmente.
seo-description: O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia que é reproduzida localmente.
seo-title: Reprodução e failover
title: Reprodução e failover
uuid: 511f16b9-2b86-42c1-8d89-09b26534200b
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Visão geral {#playback-and-failover-overview}

O streaming pela Internet requer uma conexão constante e estável para reproduzir um fluxo a partir de um servidor remoto. No entanto, a variabilidade da conexão com a Internet do visualizador ou da reprodução de streaming significa que a reprodução remota pode não ter a qualidade da mídia que é reproduzida localmente.

>[!IMPORTANT]
>
>O Primetime não pode proteger contra falhas como uma interrupção ISP ou uma desconexão de cabo.

O streaming Primetime oferece proteção contra failover para proteger a reprodução contra determinadas falhas de servidor remoto ou falhas operacionais, o que proporciona uma melhor experiência de visualização. Apesar de problemas de transmissão, o TVSDK implementa a proteção contra failover para minimizar as interrupções de reprodução e obter uma reprodução contínua. O player de vídeo muda automaticamente para um conjunto de mídia de backup quando execuções inteiras ou fragmentos não estão disponíveis.