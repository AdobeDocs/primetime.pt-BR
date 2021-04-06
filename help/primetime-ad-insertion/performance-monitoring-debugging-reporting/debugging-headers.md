---
title: Depuração de cabeçalhos
description: Depuração de cabeçalhos
copied-description: true
exl-id: 42c19089-2c61-4622-b53a-c28b8d495ef8
translation-type: tm+mt
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---

# Cabeçalhos de depuração (X-ADBE-AI-X1) {#debugging-headers}

O SSAI envia cabeçalhos HTTP que podem ser usados para coletar informações e determinar o desempenho das sessões de produção, localizadas no cabeçalho X-ADBE-AI-X1.

Exemplo de cabeçalho:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

A descrição dos campos é a seguinte:

| Nome | Descrição | Exemplo |
|--- |--- |--- |
| isActivePreroll | Se uma chamada de anúncio para precedente foi enviada | 0 |
| isAtiveMidroll | Se uma chamada de anúncio para midroll foi enviada | 3 |
| ID da solicitação | SSAI interno | 1594181097704 |
| ID da sessão | ID da sessão da solicitação | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Tipo de fluxo | u=variant, l=live, v=vod | v |
| isBootstrap | Se essa solicitação é uma chamada de bootstrap | 0 |
| Contagem de ad break | Número total de quebras de anúncio neste manifesto | 3 |
| Duração total do ad break | Duração total do ad break, em segundos | 30º |
| Contagem de chamadas de anúncio | Número de chamadas de anúncio enviadas nesta solicitação | 2 |
| Contagem de chamadas de anúncio de redirecionamento | Número de chamadas de anúncio de redirecionamento enviadas nesta solicitação | 3 |
| Duração total da chamada de anúncio | Tempo total de processamento da chamada de anúncio | 199 |
| Contagem de anúncios inserida | Número de publicidades inseridas no manifesto | 2 |
| Tempo de Solicitação de Manifesto de Origem | Tempo gasto buscando conteúdo somente | 185 |
| Tempo total de solicitação | Tempo total gasto com a busca de conteúdo e anúncios | 497 |
| Tempo de busca do manifesto do anúncio (total) | Quantidade total de tempo para buscar manifestos de anúncio | 204 |
| Tempo de busca do manifesto do anúncio (real) | Quantidade real de tempo buscando manifestos de anúncio em paralelo | 104 |
| Ocorrências do cache de conteúdo | Número de ocorrências do cache de conteúdo | 0 |
| Falha no Cache de Conteúdo | Número de erros de cache de conteúdo | 1 |
| Ad Manifest Cache Hit | Número de ocorrências de cache do manifesto de anúncio | 0 |
| Falha de cache do manifesto do anúncio | Número de erros de cache do manifesto de anúncio | 4 |
