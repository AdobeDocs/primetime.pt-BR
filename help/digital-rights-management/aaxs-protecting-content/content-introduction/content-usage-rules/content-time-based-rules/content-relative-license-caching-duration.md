---
title: Duração do cache de licenças
description: Duração do cache de licenças
copied-description: true
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Duração do cache de licenças{#license-caching-duration}

Especifica a duração em que uma licença pode ser armazenada em cache no disco no License Store local do cliente sem exigir a reaquisição do servidor de licenças. Como alternativa, você pode especificar uma data/hora absoluta após a qual uma licença não poderá mais ser armazenada em cache.

Depois que a data de expiração do cache for ultrapassada, a licença não será mais válida e o cliente deverá solicitar uma nova licença ao servidor de licenças.

Exemplo de caso de uso: use a duração do armazenamento em cache de licença para especificar uma quantidade fixa de tempo válida para uma licença específica, como em um caso de uso de aluguel. Uma locação de 30 dias pode ser especificada (com cache de licença) para indicar a duração total da licença dentro da qual o conteúdo será consumido.
