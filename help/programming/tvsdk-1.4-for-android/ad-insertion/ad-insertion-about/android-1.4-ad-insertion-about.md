---
description: A inserção de anúncios resolve anúncios de vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias ao servidor de anúncios, recebe informações sobre os anúncios do conteúdo especificado e coloca os anúncios no conteúdo em fases.
title: Inserção de anúncios
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---

# Visão geral {#insert-ads-overview}

A inserção de anúncios resolve anúncios de vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncios e reprodução de anúncios. O TVSDK faz as solicitações necessárias ao servidor de anúncios, recebe informações sobre os anúncios do conteúdo especificado e coloca os anúncios no conteúdo em fases.

Um ad break contém um ou mais anúncios reproduzidos em sequência. O TVSDK insere anúncios no conteúdo principal como membros de um ou mais ad breaks.

>[!TIP]
>
>Se o anúncio contiver erros, o TVSDK ignorará o anúncio.
