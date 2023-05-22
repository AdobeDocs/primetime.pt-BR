---
description: O TVSDK é compatível com a exclusão e substituição programática de conteúdo de anúncios em fluxos VOD.
title: Operações de intervalo de tempo personalizado
exl-id: 5480b22a-ecff-4fd8-9ec0-40e4a2e97641
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 0%

---

# Visão geral {#custom-time-range-operations-overview}

O TVSDK é compatível com a exclusão e substituição programática de conteúdo de anúncios em fluxos VOD.

O recurso de exclusão e substituição estende o recurso de marcadores de anúncios personalizados. Os marcadores de anúncios personalizados marcam seções do conteúdo principal como períodos de conteúdo relacionados a anúncios. Além de marcar esses intervalos de tempo, você também pode excluir e substituir intervalos de tempo.

<!--<a id="section_D3FE668CAF764DCC912373D5410C932C"></a>-->

A exclusão e a substituição de anúncios são implementadas com marcadores personalizados que identificam diferentes tipos de intervalos de tempo em um fluxo de VOD: marcar, excluir e substituir. Para cada intervalo de tempo personalizado, você pode executar operações associadas, incluindo exclusão ou substituição de conteúdo de anúncios.

Para exclusão e substituição de anúncios, o TVSDK inclui o seguinte *operação de intervalo de tempo personalizado* modos:

* MARK - Expedições `AdBreak` eventos para as regiões marcadas. (Isso foi chamado de `customAdMarker` em versões anteriores do TVSDK.) A inserção de anúncio não é permitida neste modo.

* DELETE - Para esse modo, o aplicativo usa o `TimeRangeCollection` classe para definir regiões de tempo para Exclusão de anúncio C3. A inserção de anúncio é permitida nesse modo.
* REPLACE - Nesse modo, o aplicativo substitui um `timeRange` com uma Adobe Primetime ad decisioning `AdBreak`. A operação de substituição começa onde a exclusão do anúncio C3 ocorre e termina no horário indicado (mais curto ou mais longo que o intervalo de tempo original).

O TVSDK fornece uma `CustomRangesOpportunityGenerator` classe para gerar oportunidades de posicionamento para os intervalos MARK e DELETE. Para o modo SUBSTITUIR, o TVSDK gera duas oportunidades de posicionamento para cada intervalo de tempo:

* A variável `CustomRangeResolver` gera oportunidades de posicionamento para o DELETE
* A variável `AuditudeAdResolver` O gera oportunidades de posicionamento para INSERT.
