---
title: Duração do cache de licenças
description: Duração do cache de licenças
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Duração do cache de licenças{#license-caching-duration}

A duração do cache de licenças especifica quanto tempo uma licença pode ser armazenada em cache no disco no License Store local do cliente sem exigir a reaquisição do servidor de licenças. Como alternativa, você pode especificar uma data e hora absolutas após as quais uma licença não poderá mais ser armazenada em cache.

Depois que a data de expiração do cache for ultrapassada, a licença não será mais válida e o cliente deverá solicitar uma nova licença ao servidor de licenças.

Exemplo de caso de uso: use a duração do armazenamento em cache de licença para especificar uma quantidade fixa de tempo válida para uma licença específica, como em um caso de uso de aluguel. Você pode especificar um aluguel de 30 dias (com licença armazenada em cache) para indicar a duração total da licença dentro da qual consumir o conteúdo.
