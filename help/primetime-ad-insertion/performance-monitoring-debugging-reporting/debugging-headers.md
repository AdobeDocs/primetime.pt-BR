---
title: Depuração de cabeçalhos
description: Depuração de cabeçalhos
copied-description: true
exl-id: 42c19089-2c61-4622-b53a-c28b8d495ef8
source-git-commit: 3e63c187f12d1bff53370bbcde4d6a77f58f3b4f
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 7%

---

# Depuração de cabeçalhos (X-ADBE-AI-X1) {#debugging-headers}

O SSAI envia cabeçalhos HTTP que podem ser usados para coletar informações e determinar o desempenho de sessões de produção, localizados no cabeçalho X-ADBE-AI-X1.

Exemplo de cabeçalho:
`X-ADBE-AI-X1: 0 1 1594181097704 15126333-5ba9-49b8-a219-4f37e60d259c v 0 1 30 2 1 199 2 185 497 204 104 0 1 0 4`

A descrição dos campos é a seguinte:

| Nome | Descrição | Exemplo |
|--- |--- |--- |
| isActivePreroll | Se uma chamada de anúncio para antes da exibição foi enviada | 0 |
| isActiveMidroll | Se uma chamada de anúncio para a exibição intermediária foi enviada | 1 |
| ID da solicitação | SSAI interno | 1594181097704 |
| ID da sessão | ID de sessão da solicitação | 15126333-5ba9-49b8-a219-4f37e60d259c |
| Tipo de fluxo | u=variante, l=live, v=vod | v |
| isBootstrap | Se esta solicitação é uma chamada de inicialização | 0 |
| Contagem de ad break | Número total de ad breaks neste manifesto | 1 |
| Duração total do ad break | Duração total do ad break, em segundos | 30 |
| Contagem de chamadas de anúncio | Número de chamadas de publicidade enviadas nesta solicitação | 2 |
| Contagem de chamadas de anúncio de redirecionamento | Número de chamadas de publicidade de redirecionamento enviadas nesta solicitação | 1 |
| Duração total da chamada do anúncio | Tempo total de processamento de chamadas de anúncio | 199 |
| Contagem de anúncios inseridos | Número de anúncios inseridos no manifesto | 2 |
| Tempo de Solicitação do Manifesto de Origem | Tempo gasto na busca somente de conteúdo | 185 |
| Tempo total de solicitação | Tempo total gasto na busca de conteúdo e anúncios | 497 |
| Tempo de busca do manifesto publicitário (total) | Quantidade total de tempo para obtenção de manifestos de anúncios | 204 |
| Tempo de busca do manifesto publicitário (real) | Quantidade real de tempo para obtenção de manifestos de anúncio em paralelo | 104 |
| Acertos do cache de conteúdo | Número de ocorrências do cache de conteúdo | 0 |
| Erro de cache de conteúdo | Número de erros do cache de conteúdo | 1 |
| Acerto do Cache de Manifesto de Anúncio | Número de acertos do cache do manifesto de anúncio | 0 |
| Erro de cache do manifesto de anúncio | Número de erros do cache do manifesto de anúncio | 4 |
