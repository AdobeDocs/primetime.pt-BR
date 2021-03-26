---
title: Anúncios de Ad Insertion Adobe Primetime
description: Anúncios sobre lançamentos de recursos recentes e outras notícias relacionadas sobre o Primetime Ad Insertion
translation-type: tm+mt
source-git-commit: d8fde0d03bea85b3fefcfa5dcbfddee76b17de03
workflow-type: tm+mt
source-wordcount: '307'
ht-degree: 0%

---


# Anúncios de Ad Insertion do Primetime

## Redução de erros de anúncios programáticos por meio de tempos limite de resolução de anúncios

Publicado em 1 de dezembro de 2020

O Adobe tem como foco ajudar nossos clientes do Ad Insertion Primetime a maximizar a monetização de seu inventário de anúncios. Prestamos especial atenção à redução da complexidade de atender à demanda programática, que representa mais de três quartos dos gastos com vídeo eMarketer dos EUA. A venda programática permite que os editores maximizem a demanda de seu inventário de anúncios, levando a maiores taxas de preenchimento e rendimento. Mas também aumenta a exposição a erros de anúncio, como respostas VAST malformadas, erros HTTP e outros que podem levar à perda de receita e/ou a experiências ruins do visualizador.

Um problema comum é a lentidão das respostas de anúncios dos parceiros programáticos. Normalmente, as transações de anúncios programáticas ocorrem em milissegundos. No entanto, às vezes, uma única fonte de demanda pode demorar muito para responder. Um atraso de um único provedor pode afetar todo o processo de preenchimento do anúncio, causando telas em branco temporárias para o visualizador, slots de anúncio não preenchidos ou, em casos extremos, a necessidade de reiniciar um fluxo de vídeo. Infelizmente, identificar e ignorar fontes de procura lentas é um grande desafio.

Para solucionar esse problema, o Adobe adicionou novas ferramentas ao Primetime Ad Insertion que permitem aos clientes definir restrições de tempo para a resolução do anúncio. Definir essas regras faz com que fontes de demanda lentas sejam ignoradas automaticamente, garantindo que os players de vídeo obtenham respostas de anúncio em tempo hábil. Isso permite que os editores limitem bastante as interrupções de fontes de demanda lentas, ajudando-os a maximizar as taxas de preenchimento do inventário e a fornecer experiências de exibição ininterruptas e com qualidade de TV.

Para ativar o tempo limite da resolução do anúncio no Primetime Ad Insertion, modifique as APIs de inicialização para incluir o parâmetro ptadtimeout (duração em milissegundos).  As solicitações de anúncios que não forem concluídas antes da duração do tempo limite não serão compiladas (quaisquer anúncios de fallback serão processados).