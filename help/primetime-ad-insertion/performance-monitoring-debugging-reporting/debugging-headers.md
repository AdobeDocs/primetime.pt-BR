---
title: Depuração de cabeçalhos
description: null
translation-type: tm+mt
source-git-commit: 45e5c8e6144adf4a405bde7d8d19505b7ad549e0
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 7%

---


# Cabeçalhos de depuração (X-ADBE-AI-X1) {#debugging-headers}

O SSAI envia cabeçalhos HTTP que podem ser usados para coletar informações e determinar o desempenho das sessões de produção, localizadas no cabeçalho X-ADBE-AI-X1.

Exemplo de cabeçalho:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

A descrição dos campos é a seguinte:

| Nome | Descrição | Exemplo |
|--- |--- |--- |
| isActivePreroll | Se uma chamada de anúncio para pre-roll foi enviada | 0 |
| isActiveMidroll | Se uma chamada de anúncio para midroll foi enviada | 1 |
| ID da solicitação | SSAI interno | 1594181097704 |
| ID da sessão | ID da sessão da solicitação | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Tipo de fluxo | u=variant, l=live, v=vod | v |
| isBootstrap | Se essa solicitação é uma chamada de inicialização | 0 |
| Contagem de quebras de anúncios | Número total de quebras de anúncio neste manifesto | 1 |
| Duração total do intervalo do anúncio | Duração total do intervalo do anúncio, em segundos | 30 |
| Contagem de chamadas de anúncio | Número de chamadas de anúncio enviadas nesta solicitação | 2 |
| Contagem de chamadas de anúncio de redirecionamento | Número de chamadas de anúncio de redirecionamento enviadas nesta solicitação | 3 |
| Duração total da chamada de anúncio | Tempo total de processamento da chamada de anúncio | 199 |
| Contagem de anúncios inserida | Número de publicidades inseridas no manifesto | 2 |
| Tempo de solicitação do manifesto de origem | Tempo gasto buscando somente conteúdo | 185 |
| Tempo total de solicitação | Tempo total gasto na busca de conteúdo e anúncios | 497 |
| Tempo de busca do manifesto do anúncio (total) | Tempo total para buscar manifestos de anúncio | 204 |
| Tempo de busca do manifesto do anúncio (real) | Tempo real de busca de manifestos de anúncio em paralelo | 104 |
| Ocorrências do cache de conteúdo | Número de ocorrências do cache de conteúdo | 0 |
| Falta de Cache de Conteúdo | Número de erros de cache de conteúdo | 1 |
| Acerto no cache do manifesto do anúncio | Número de ocorrências de cache do manifesto do anúncio | 0 |
| Falha de cache de manifesto do anúncio | Número de falhas de cache do manifesto do anúncio | 4 |