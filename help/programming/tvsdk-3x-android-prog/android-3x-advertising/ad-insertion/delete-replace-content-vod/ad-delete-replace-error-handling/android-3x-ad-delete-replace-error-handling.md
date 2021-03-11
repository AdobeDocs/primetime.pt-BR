---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico ao mesclar ou reordenar os intervalos de tempo definidos incorretamente.
title: Exclusão de anúncios e tratamento de erros de substituição
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---


# Erro de exclusão e substituição de anúncio que manipula {#ad-deletion-and-replacement-error-handling}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico ao mesclar ou reordenar os intervalos de tempo definidos incorretamente.

O TVSDK gerencia erros `timeRanges` por meio de processos padrão de mesclagem e reordenação. Primeiro, o reprodutor classifica os intervalos de tempo definidos pelo cliente de acordo com a hora *begin*. Com base nessa ordem de classificação, se houver subconjuntos e interseções entre os intervalos, o TVSDK mesclará intervalos adjacentes e unirá esses intervalos.

O TVSDK lida com erros de intervalo de tempo com as seguintes opções:

* **Fora do** orderTVSDK reorganiza os intervalos de tempo.

* **** SubsetTVSDK mescla os subconjuntos de intervalo de tempo.

* **** IntersectTVSDK mescla os intervalos de tempo de interseção.

* **Substituir intervalos** conflictTVSDK seleciona a duração de substituição da mais antiga  `timeRange` que aparece no grupo conflitante.

O TVSDK lida com conflitos do modo de sinalização com metadados de anúncio das seguintes maneiras:

* Se o modo de sinalização do anúncio estiver em conflito com os metadados do intervalo de tempo, os metadados do intervalo de tempo sempre terão prioridade.

   Por exemplo, se o modo de sinalização do anúncio estiver definido como mapa do servidor ou dicas de manifesto e também houver intervalos de tempo MARK nos metadados do anúncio, o comportamento resultante será que os intervalos estão marcados e nenhum anúncio será inserido.
* Para intervalos REPLACE, se o modo de sinalização estiver definido como o mapa do servidor ou as dicas de manifesto, os intervalos serão substituídos conforme especificado nos intervalos REPLACE, e não haverá inserção de anúncio por meio do mapa do servidor ou das dicas de manifesto.

   Para obter mais informações, consulte a tabela *Modo de sinalização / Comportamentos de combinação de metadados* em [Efeito na inserção e exclusão de anúncios no modo de sinalização de anúncios](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md).

Lembre-se do seguinte:

* Quando o servidor não retorna um `AdBreaks` válido, o TVSDK gera e processa um `NOPTimelineOperation` para o AdBreak vazio, e nenhum anúncio é reproduzido.

* Embora a exclusão/substituição de anúncios C3 deva ser aceita apenas para VOD, se especificados nos metadados do anúncio, os intervalos de tempo também são processados para fluxos ao vivo.
