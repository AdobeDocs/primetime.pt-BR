---
title: Anúncios do Ad Insertion Adobe Primetime
seo-title: Anúncios do Ad Insertion Adobe Primetime
description: Anúncios sobre lançamentos recentes e outras notícias relacionadas sobre o Primetime Ad Insertion
seo-description: Anúncios sobre lançamentos recentes e outras notícias relacionadas sobre o Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: d5e948992d7c59e80b530c8f4619adbffc3c03d8
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 0%

---


# Anúncios do Primetime Ad Insertion

## Redução de erros de anúncios programáticos por meio de tempos limite de resolução de anúncios

Publicado em 1 de dezembro de 2000

O Adobe está focado em ajudar nossos clientes do Primetime Ad Insertion a maximizar a monetização de seu inventário de anúncios. Prestamos especial atenção à redução das complexidades do cumprimento da demanda programática, que representa mais de três quartos dos gastos com vídeos digitais dos EUA, de acordo com o eMarketer. A venda programática permite que os editores maximizem a demanda para seu inventário de anúncios, levando a taxas de preenchimento e rendimento mais altos. Mas também aumenta a exposição a erros de anúncio, como respostas VAST mal formadas, erros HTTP e outros que podem levar a perda de receita e/ou a experiências ruins do visualizador.

Um problema comum é a lentidão das respostas dos parceiros programáticos. Normalmente, as transações de anúncios programáticas ocorrem em milissegundos. No entanto, algumas vezes uma única fonte de demanda pode levar um tempo excessivo para responder. Um atraso de um único provedor pode afetar todo o processo de preenchimento do anúncio, causando telas em branco temporárias para o visualizador, slots de anúncio não preenchidos ou, em casos extremos, a necessidade de reiniciar um fluxo de vídeo. Infelizmente, identificar e ignorar fontes de procura lentas é um grande desafio.

Para solucionar esse problema, o Adobe adicionou novas ferramentas ao Primetime Ad Insertion que permitem que os clientes definam restrições de tempo para a resolução do anúncio. A definição dessas regras faz com que as fontes de demanda lentas sejam ignoradas automaticamente, garantindo que os players de vídeo obtenham respostas de anúncios em tempo hábil. Isso permite que os editores limitem consideravelmente as interrupções de fontes de demanda lenta, ajudando-os a maximizar as taxas de preenchimento do inventário e a fornecer experiências de exibição ininterruptas e com qualidade de TV.

Para ativar o tempo limite de resolução de anúncio no Primetime Ad Insertion, modifique as APIs de inicialização para incluir o parâmetro ptadtimeout (duração em milissegundos).  Quaisquer solicitações de anúncios que não forem concluídas antes da duração do tempo limite não serão agrupadas (quaisquer anúncios de fallback serão processados).