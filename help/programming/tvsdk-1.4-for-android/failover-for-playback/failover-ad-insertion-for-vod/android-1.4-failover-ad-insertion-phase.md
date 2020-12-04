---
description: O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.
seo-description: O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.
seo-title: Fase de inserção de anúncios
title: Fase de inserção de anúncios
uuid: 4a8e9578-6e95-44c0-b045-ae3c20da75e9
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---


# Fase de inserção de anúncio{#ad-insertion-phase}

O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios estiver concluída, o TVSDK terá uma lista ordenada de recursos de anúncios que são agrupados em quebras de anúncios. Cada quebra de anúncio é posicionada na linha do tempo do conteúdo principal usando um valor de start-tempo que é expresso em milissegundos (ms). Cada anúncio em uma quebra de anúncio tem uma propriedade de duração que também é expressa em ms. Os anúncios em intervalos de anúncios são encadeados um após o outro. Como resultado, a duração de um intervalo de anúncios é igual à soma das durações dos anúncios individuais que compõem os anúncios.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de tempo/duração de start de quebra de anúncio, os segmentos de anúncio podem se sobrepor. A sobreposição ocorre quando a última parte de um intervalo de anúncios faz interseção com o início do primeiro anúncio no próximo intervalo de anúncios. Nessas situações, o TVSDK descarta o intervalo posterior do anúncio e continua o processo de inserção do anúncio com o próximo item na lista até que todas as quebras do anúncio sejam inseridas ou descartadas.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.
