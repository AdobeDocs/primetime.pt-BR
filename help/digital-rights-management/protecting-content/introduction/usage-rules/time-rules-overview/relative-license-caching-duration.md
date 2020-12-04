---
seo-title: Duração do armazenamento em cache da licença
title: Duração do armazenamento em cache da licença
uuid: d448aa43-8cba-4b1d-8609-0dba4bb67042
translation-type: tm+mt
source-git-commit: 29bc8323460d9be0fce66cbea7c6fce46df20d61
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Duração do armazenamento em cache da licença{#license-caching-duration}

A duração do armazenamento em cache de licenças especifica por quanto tempo uma licença pode ser armazenada em cache no disco do Repositório de Licenças local do cliente sem a necessidade de reaquisição do servidor de licenças. Como alternativa, você pode especificar uma data e hora absolutas após as quais uma licença não pode mais ser armazenada em cache.

Depois que a data de expiração do cache for ultrapassada, a licença não será mais válida e o cliente deverá solicitar uma nova licença do servidor de licenças.

Exemplo de caso de uso: Use a duração do armazenamento em cache da licença para especificar um período fixo válido para uma licença específica, como em um caso de uso de aluguel. Você pode especificar um aluguel de 30 dias (com armazenamento em cache de licenças) para indicar a duração total da licença para consumir o conteúdo.
