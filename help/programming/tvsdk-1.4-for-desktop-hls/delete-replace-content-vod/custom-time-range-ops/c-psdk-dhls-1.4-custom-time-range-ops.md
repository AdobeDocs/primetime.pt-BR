---
description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-title: Operações de intervalo de tempo personalizado
title: Operações de intervalo de tempo personalizado
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 0%

---


# Visão geral {#custom-time-range-operations-overview}

O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.

O recurso excluir e substituir estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionados a anúncios. Além de marcar esses intervalos de tempo, também é possível excluir e substituir intervalos de tempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

A exclusão e substituição de anúncios são implementadas com marcadores personalizados que identificam diferentes tipos de intervalos de tempo em um fluxo VOD: marcar, excluir e substituir. Para cada intervalo de tempo personalizado, é possível executar operações associadas, incluindo a exclusão ou substituição do conteúdo do anúncio.

Para exclusão e substituição de anúncios, o TVSDK inclui os seguintes modos *operação de intervalo de tempo personalizado*:

* MARK - despacha eventos `AdBreak` para as regiões marcadas. (Isso foi chamado `customAdMarker` em versões anteriores do TVSDK.) A inserção de publicidade não é permitida neste modo.

* DELETE - Nesse modo, o aplicativo usa a classe `TimeRangeCollection` para definir regiões de tempo para a exclusão de anúncios C3. A inserção de publicidade é permitida neste modo.
* REPLACE - Nesse modo, o aplicativo substitui `timeRange` por uma decisão de anúncio da Adobe Primetime `AdBreak`. A operação de substituição start onde a exclusão do anúncio C3 ocorre e termina no tempo indicado (menor ou maior que o intervalo de tempo original).

O TVSDK fornece uma classe `CustomRangesOpportunityGenerator` para gerar oportunidades de colocação para os intervalos MARK e DELETE. Para o modo REPLACE, o TVSDK gera duas oportunidades de colocação para cada intervalo de tempo:

* O `CustomRangeResolver` gera oportunidades de colocação para o DELETE
* O `AuditudeAdResolver` gera oportunidades de colocação para INSERT.