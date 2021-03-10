---
description: O TVSDK oferece suporte à exclusão programática e substituição de conteúdo de anúncio em fluxos VOD.
title: Operações de intervalo de tempo personalizado
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---


# Visão geral {#custom-time-range-operations-overview}

O TVSDK oferece suporte à exclusão programática e substituição de conteúdo de anúncio em fluxos VOD.

O recurso excluir e substituir estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionado a anúncios. Além de marcar esses intervalos de tempo, também é possível excluir e substituir intervalos de tempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

A exclusão e substituição de anúncios são implementadas com marcadores personalizados que identificam diferentes tipos de intervalos de tempo em um fluxo de VOD: marcar, excluir e substituir. Para cada intervalo de tempo personalizado, é possível executar operações associadas, incluindo a exclusão ou substituição do conteúdo do anúncio.

Para exclusão e substituição de anúncios, o TVSDK inclui os seguintes modos *operação de intervalo de tempo personalizado*:

* MARK - Envia eventos `AdBreak` para as regiões marcadas. (Isso era chamado de `customAdMarker` em versões anteriores do TVSDK.) A inserção de anúncio não é permitida neste modo.

* DELETE - Para esse modo, o aplicativo usa a classe `TimeRangeCollection` para definir regiões de tempo para a Exclusão de anúncio C3. A inserção de anúncio é permitida nesse modo.
* SUBSTITUIR - Nesse modo, o aplicativo substitui um `timeRange` por um Adobe Primetime ad decisioning `AdBreak`. A operação de substituição começa onde a exclusão do anúncio C3 ocorre e termina no tempo indicado (menor ou maior que o intervalo de tempo original).

O TVSDK fornece uma classe `CustomRangesOpportunityGenerator` para gerar oportunidades de posicionamento para os intervalos MARK e DELETE. Para o modo REPLACE, o TVSDK gera duas oportunidades de posicionamento para cada intervalo de tempo:

* O `CustomRangeResolver` gera oportunidades de posicionamento para o DELETE
* O `AuditudeAdResolver` gera oportunidades de posicionamento para INSERT.