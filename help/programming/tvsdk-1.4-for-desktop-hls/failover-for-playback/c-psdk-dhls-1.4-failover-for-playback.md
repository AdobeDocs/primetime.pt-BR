---
description: A transmissão pela Internet requer uma conexão constante e estável para reproduzir um fluxo de um servidor remoto. No entanto, a variabilidade da conexão de Internet ou da reprodução de streaming de um visualizador significa que a reprodução remota pode não ter a qualidade de mídia reproduzida localmente.
title: Reprodução e failover
exl-id: 45693d0b-a5fb-4716-a410-ac323950f40b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Visão geral {#playback-and-failover-overview}

A transmissão pela Internet requer uma conexão constante e estável para reproduzir um fluxo de um servidor remoto. No entanto, a variabilidade da conexão de Internet ou da reprodução de streaming de um visualizador significa que a reprodução remota pode não ter a qualidade de mídia reproduzida localmente.

O Primetime não pode proteger contra falhas como interrupção do ISP ou desconexão de cabo. No entanto, a transmissão contínua do Primetime fornece proteção contra failover para proteger a reprodução de determinadas falhas de servidor remoto ou falhas operacionais, proporcionando uma melhor experiência aos visualizadores. O TVSDK implementa a proteção contra failover para minimizar as interrupções da reprodução e obter uma reprodução contínua apesar dos problemas de transmissão. O reprodutor de vídeo alterna automaticamente para um conjunto de mídia de backup quando representações ou fragmentos inteiros não estão disponíveis.
