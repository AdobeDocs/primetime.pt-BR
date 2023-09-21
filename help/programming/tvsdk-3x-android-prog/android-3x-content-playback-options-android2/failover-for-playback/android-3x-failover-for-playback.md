---
description: A transmissão pela Internet requer uma conexão constante e estável para reproduzir um fluxo de um servidor remoto. No entanto, devido à variabilidade da conexão de Internet ou da reprodução de streaming de um visualizador, a reprodução remota pode não ter a qualidade de mídia reproduzida localmente.
title: Reprodução e failover
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '161'
ht-degree: 0%

---

# Visão geral {#playback-and-failover-overview}

A transmissão pela Internet requer uma conexão constante e estável para reproduzir um fluxo de um servidor remoto. No entanto, devido à variabilidade da conexão de Internet ou da reprodução de streaming de um visualizador, a reprodução remota pode não ter a qualidade de mídia reproduzida localmente.

>[!IMPORTANT]
>
>O Primetime não pode proteger contra falhas como uma interrupção do ISP ou uma desconexão de cabo.

A transmissão contínua do Primetime fornece proteção contra failover para proteger a reprodução contra determinadas falhas de servidor remoto ou falhas operacionais, o que torna a experiência de visualização melhor. Apesar dos problemas de transmissão, o TVSDK implementa a proteção contra failover para minimizar as interrupções da reprodução e obter uma reprodução contínua. O reprodutor de vídeo alterna automaticamente para um conjunto de mídia de backup quando representações ou fragmentos inteiros não estão disponíveis.
