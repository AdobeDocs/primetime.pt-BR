---
description: O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.
title: Fase de inserção do anúncio
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%

---

# Fase de inserção do anúncio{#ad-insertion-phase}

O TVSDK insere o conteúdo alternativo (anúncios) na linha do tempo que corresponde ao conteúdo principal.

Quando a fase de resolução de anúncios for concluída, o TVSDK terá uma lista ordenada de recursos de anúncios agrupados em ad breaks. Cada ad break é posicionado na linha do tempo do conteúdo principal usando um valor de hora de início expresso em milissegundos (ms). Cada anúncio em um ad break tem uma propriedade de duração que também é expressa em ms. Os anúncios em um ad break são encadeados um após o outro. Como resultado, a duração de um ad break é igual à soma das durações dos anúncios compostos individuais.

O failover pode ocorrer nesta fase com conflitos que podem ocorrer na linha do tempo durante a inserção do anúncio. Para combinações específicas de valores de hora de início/duração do ad break, os segmentos de anúncios podem se sobrepor. A sobreposição ocorre quando a última parte de um ad break intercepta o início do primeiro anúncio no próximo ad break. Nessas situações, o TVSDK descarta o ad break posterior e continua o processo de inserção de anúncios com o próximo item na lista até que todos os ad breaks sejam inseridos ou descartados.

O TVSDK emite uma notificação de aviso sobre o erro e continua o processamento.
