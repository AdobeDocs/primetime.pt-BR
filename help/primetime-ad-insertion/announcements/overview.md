---
title: Anúncios do Adobe Primetime Ad Insertion
description: Anúncios sobre lançamentos recentes de recursos e outras notícias relacionadas sobre Primetime Ad Insertion
exl-id: 7d85d3a2-6786-47bd-8d45-ec162aea0ab3
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---

# Anúncios de Ad Insertion do Primetime

## Redução de erros programáticos de anúncios por meio do tempo limite de resolução de anúncios

Publicado em 1 de dezembro de 2020

O foco do Adobe é ajudar nossos clientes do Primetime Ad Insertion a maximizar a monetização de seu inventário de anúncios. Prestamos atenção especial à redução das complexidades de atender à demanda programática, que representa mais de três quartos dos gastos com anúncios de vídeo digital nos EUA, de acordo com o eMarketer. A venda programática permite que os editores maximizem a demanda para o inventário de anúncios, resultando em taxas de preenchimento e rendimento mais altos. Mas também aumenta a exposição a erros de anúncio, como respostas VAST malformadas, erros HTTP e outros que podem levar a perda de receita e/ou experiências de visualizador inadequadas.

Um problema comum é a lentidão e as respostas de parceiros programáticos. Normalmente, as transações de anúncios programáticas ocorrem em milissegundos. No entanto, às vezes, uma única fonte de demanda pode levar um tempo excessivo para responder. Um atraso de um único provedor pode afetar todo o processo de preenchimento de anúncios, causando telas em branco temporárias para o visualizador, slots de anúncios não preenchidos ou, em casos extremos, a necessidade de reiniciar um fluxo de vídeo. Infelizmente, identificar e contornar as fontes de demanda lenta é um grande desafio.

Para resolver esse problema, o Adobe adicionou novas ferramentas ao Ad Insertion do Primetime, que permitem que os clientes definam restrições de tempo para a resolução de anúncios. A definição dessas regras faz com que as fontes de demanda lenta sejam ignoradas automaticamente, garantindo que os players de vídeo obtenham respostas de anúncio em tempo hábil. Isso permite que os editores limitem bastante as interrupções de fontes de demanda lenta, ajudando-os a maximizar as taxas de preenchimento de inventário e a fornecer experiências de visualização ininterruptas com qualidade de TV.

Para ativar o tempo limite da resolução do anúncio no Ad Insertion do Primetime, modifique as APIs de inicialização para incluir o parâmetro ptadtimeout (duração em milissegundos).  Qualquer solicitação de anúncio que não for concluída antes do tempo limite não será compilada (qualquer anúncio de fallback será processado).
