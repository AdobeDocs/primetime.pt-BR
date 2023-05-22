---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico mesclando ou reorganizando os intervalos de tempo definidos incorretamente.
title: Tratamento de erros de exclusão e substituição de anúncios
exl-id: 0d70bb63-bdc5-4741-81db-1408216234c2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Visão geral {#ad-deletion-and-replacement-error-handling-overview}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico mesclando ou reorganizando os intervalos de tempo definidos incorretamente.

O TVSDK gerencia `timeRanges` erros por meio de processos padrão de mesclagem e reordenação. Primeiro, o reprodutor classifica os intervalos de tempo definidos pelo cliente pela variável *start* hora. Com base nessa ordem de classificação, se houver subconjuntos e interseções entre os intervalos, o TVSDK mesclará intervalos adjacentes e unirá esses intervalos.

O TVSDK lida com erros de intervalo de tempo com as seguintes opções:

* **Fora de ordem** O TVSDK reorganiza os intervalos de tempo.

* **Subconjunto** O TVSDK mescla os subconjuntos de intervalo de tempo.

* **Interseção** O TVSDK mescla os intervalos de tempo de interseção.

* **Substituir conflito de intervalos** O TVSDK seleciona a duração de substituição a partir da mais antiga `timeRange` que aparece no grupo conflitante.

O TVSDK lida com conflitos do modo de sinalização com metadados de anúncio das seguintes maneiras:

* Se o modo de sinalização de anúncios entrar em conflito com os metadados de intervalo de tempo, os metadados de intervalo de tempo sempre terão prioridade.

   Por exemplo, se o modo de sinalização de anúncios estiver definido como mapa do servidor ou dicas de manifesto e também houver intervalos de tempo MARCAR nos metadados do anúncio, o comportamento resultante será que os intervalos estão marcados e nenhum anúncio foi inserido.
* Para intervalos REPLACE, se o modo de sinalização estiver definido como o mapa do servidor ou as dicas do manifesto, os intervalos serão substituídos conforme especificado nos intervalos REPLACE e não haverá inserção de anúncio por meio do mapa do servidor ou das dicas do manifesto.

   Para obter mais informações, consulte *Comportamentos de combinação de modo de sinalização/metadados* tabela em [Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios...](../../../../tvsdk-2.7-for-android/ad-insertion/delete-replace-content-vod/c-psdk-android-2.7-signaling-mode-metadata-combos-android.md#c_psdk_signaling-mode-metadata-combos-android).

Lembre-se do seguinte:

* Quando o servidor não retornar válido `AdBreaks`, o TVSDK gera e processa um `NOPTimelineOperation` para o AdBreak vazio e nenhum anúncio é reproduzido.

* Embora a intenção seja que o anúncio C3 seja excluído/substituído somente para VOD, se especificado nos metadados do anúncio, os intervalos de tempo também são processados para fluxos em tempo real.
