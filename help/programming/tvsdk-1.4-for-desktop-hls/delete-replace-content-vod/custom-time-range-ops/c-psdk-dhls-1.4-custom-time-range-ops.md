---
description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-description: O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.
seo-title: Operações de intervalo de tempo personalizado
title: Operações de intervalo de tempo personalizado
uuid: fb27f343-718d-444e-8fc1-5ae0be02557b
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Visão geral {#custom-time-range-operations-overview}

O TVSDK oferece suporte à exclusão e substituição programática de conteúdo de anúncio em fluxos VOD.

O recurso excluir e substituir estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionados a anúncios. Além de marcar esses intervalos de tempo, também é possível excluir e substituir intervalos de tempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

A exclusão e substituição de anúncios são implementadas com marcadores personalizados que identificam diferentes tipos de intervalos de tempo em um fluxo VOD: marcar, excluir e substituir. Para cada intervalo de tempo personalizado, é possível executar operações associadas, incluindo a exclusão ou substituição do conteúdo do anúncio.

Para exclusão e substituição de anúncios, o TVSDK inclui os seguintes modos de operação *de intervalo de tempo* personalizado:

* MARK - Envia `AdBreak` eventos para as regiões marcadas. (Isso foi chamado `customAdMarker` em versões anteriores do TVSDK.) A inserção de publicidade não é permitida neste modo.

* EXCLUIR - Para este modo, o aplicativo usa a `TimeRangeCollection` classe para definir regiões de tempo para a exclusão de anúncios C3. A inserção de publicidade é permitida neste modo.
* SUBSTITUIR - Nesse modo, o aplicativo substitui um anúncio `timeRange` por uma decisão do Adobe Primetime `AdBreak`. A operação de substituição começa no local em que a exclusão do anúncio C3 ocorre e termina no horário indicado (menor ou maior que o intervalo de tempo original).

O TVSDK fornece uma `CustomRangesOpportunityGenerator` classe para gerar oportunidades de posicionamento para os intervalos MARK e DELETE. Para o modo REPLACE, o TVSDK gera duas oportunidades de colocação para cada intervalo de tempo:

* O `CustomRangeResolver` gera oportunidades de posicionamento para EXCLUIR
* O `AuditudeAdResolver` gera oportunidades de colocação para INSERT.