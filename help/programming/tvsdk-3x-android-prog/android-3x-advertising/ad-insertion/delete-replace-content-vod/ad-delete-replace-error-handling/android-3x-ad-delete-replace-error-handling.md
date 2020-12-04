---
description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico ao mesclar ou reordenar os intervalos de tempo definidos incorretamente.
seo-description: O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico ao mesclar ou reordenar os intervalos de tempo definidos incorretamente.
seo-title: Tratamento de erros de exclusão e substituição de anúncios
title: Tratamento de erros de exclusão e substituição de anúncios
uuid: 615f42b7-733a-49c4-bd7a-f14ad0d23fa0
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---


# Exclusão de anúncios e tratamento de erros de substituição {#ad-deletion-and-replacement-error-handling}

O TVSDK lida com erros de intervalo de tempo de acordo com o problema específico ao mesclar ou reordenar os intervalos de tempo definidos incorretamente.

O TVSDK gerencia erros `timeRanges` por meio de processos padrão de mesclagem e reordenação. Primeiro, o player classifica os intervalos de tempo definidos pelo cliente de acordo com a hora *begin*. Com base nessa ordem de classificação, se houver subconjuntos e interseções entre os intervalos, o TVSDK mesclará intervalos adjacentes e unirá esses intervalos.

O TVSDK lida com erros de intervalo de tempo com as seguintes opções:

* **Fora do** pedidoO TVSDK reorganiza os intervalos de tempo.

* **O** SubsetTVSDK mescla os subconjuntos de intervalo de tempo.

* **O** IntersectTVSDK mescla os intervalos de tempo de interseção.

* **Substituir intervalos** conflitoO TVSDK seleciona a duração da substituição da mais antiga  `timeRange` que aparece no grupo em conflito.

O TVSDK lida com conflitos de modo de sinalização com metadados de anúncio das seguintes maneiras:

* Se o modo de sinalização de anúncio estiver em conflito com os metadados do intervalo de tempo, os metadados do intervalo de tempo sempre terão prioridade.

   Por exemplo, se o modo de sinalização de anúncio estiver definido como mapa do servidor ou dicas de manifesto e também houver intervalos de tempo MARK nos metadados do anúncio, o comportamento resultante será que os intervalos estejam marcados e nenhum anúncio será inserido.
* Para intervalos REPLACE, se o modo de sinalização estiver definido como o mapa do servidor ou as dicas do manifesto, os intervalos serão substituídos conforme especificado nos intervalos REPLACE e não haverá inserção de anúncio por meio do mapa do servidor ou das dicas do manifesto.

   Para obter mais informações, consulte a tabela *Modo de sinalização / Comportamentos de combinação de metadados* em [Efeito na inserção e exclusão de anúncios do modo de sinalização de anúncios](../../../../../tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/delete-replace-content-vod/android-3x-signaling-mode-android.md).

Lembre-se do seguinte:

* Quando o servidor não retorna um `AdBreaks` válido, o TVSDK gera e processa um `NOPTimelineOperation` para o AdBreak vazio, e nenhum anúncio é reproduzido.

* Embora C3 e delete/replace sejam destinados ao suporte somente para VOD, se especificados nos metadados do anúncio, os intervalos de tempo também são processados para fluxos ao vivo.
