---
description: A inserção de anúncio resolve os anúncios de vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncio e reprodução de anúncio. O TVSDK faz as solicitações necessárias para o servidor de publicidade, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios em fases.
title: Inserção de anúncios
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 0%

---


# Visão geral {#insert-ads-overview}

A inserção de anúncio resolve os anúncios de vídeo sob demanda (VOD), para transmissão ao vivo e para transmissão linear com rastreamento de anúncio e reprodução de anúncio. O TVSDK faz as solicitações necessárias para o servidor de publicidade, recebe informações sobre anúncios para o conteúdo especificado e coloca os anúncios em fases.

Um ad break contém um ou mais anúncios que são exibidos em sequência. O TVSDK insere anúncios no conteúdo principal como membros de um ou mais ad breaks.

>[!TIP]
>
>Se o anúncio tiver erros, o TVSDK ignorará o anúncio.