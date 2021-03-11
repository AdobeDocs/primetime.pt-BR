---
title: Duração do armazenamento em cache de licenças
description: Duração do armazenamento em cache de licenças
copied-description: true
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Duração do armazenamento em cache de licenças{#license-caching-duration}

Especifica a duração em que uma licença pode ser armazenada em cache no disco no License Store local do cliente sem exigir reaquisição do servidor de licença. Como alternativa, você pode especificar uma data/hora absoluta após a qual uma licença não pode mais ser armazenada em cache.

Depois que a data de expiração do cache tiver passado, a licença não será mais válida e o cliente deverá solicitar uma nova licença do servidor de licenças.

Exemplo de caso de uso: Use a duração do armazenamento em cache de licenças para especificar um período fixo válido para uma licença específica, como em um caso de uso de aluguel. É possível especificar um aluguel de 30 dias (com armazenamento em cache de licenças) para indicar a duração total da licença dentro da qual consumir o conteúdo.
