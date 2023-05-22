---
description: Essas alterações no TVSDK oferecem suporte à exclusão e substituição de anúncios.
title: Alterações na exclusão de anúncios e na API de substituição
exl-id: 3cf63353-741b-41f4-93fd-609b69f7c3af
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Alterações na exclusão de anúncios e na API de substituição {#ad-deletion-and-replacement-api-changes}

Essas alterações no TVSDK oferecem suporte à exclusão e substituição de anúncios.

* `AdSignalingMode` Adicionado `CUSTOM_RANGES` modo de sinalização.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Definir `AdSignalingMode.CUSTOM_RANGES` se os intervalos de substituição estiverem nos metadados.

* `PlacementType` Adicionado `CUSTOM_RANGE` tipo.

* `PlacementMode`

   * Adicionado `DELETE` modo.
   * Adicionado `MARK` modo
   * Adicionado `FreeReplace` mode - este modo tem uma duração, mas é uma inserção pura

* `TimeRange` Não é mais um `final` classe

* Adicionado `ReplaceTimeRange()` método

   Estende `TimeRange` para ter uma `replacementDuration` propriedade. Nos processos MARK e DELETE, `replacementDuration` é 0.

* `TimeRangeCollection`

   * Adicionado `toReplaceMetadata()` função de utilitário a ser extraída `timeRanges`.

   * Modificado para trabalhar com `DELETE` e `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Adicionado `createCustomTimeRangesFrom()` - Cria metadados para casos de uso MARK/DELETE/REPLACE a partir do arquivo JSON.
   * Removido `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Adicionado `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Adicionado `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (não foi alterado)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Adicionado `CustomRangesOpportunityGenerator` para quando os metadados contêm intervalos personalizados
   * `doRetrieveResolvers()`

      * Adicionar `CustomRangeResolver` para quando intervalos personalizados de DELETE e REPLACE estiverem presentes nos metadados
      * Movido `CustomAdMarkerResolver` antes de `AuditudeResolver`


* Adicionado `CustomRangeOpportunityGenerator`

   * `doUpdate()` Deixa em branco - sem atualização, VOD
   * `doProcess()` Cria um novo posicionamento de um novo tipo `Placement.Delete_Range`

   * Adicionado `CustomRangeOppotunityGenerator` no topo da lista geradores em `DefaultContentFactory`, portanto, os intervalos de exclusão são processados antes das inserções de anúncios.

   * Adicionado `createCustomRangeOpportunities` para criar todas as oportunidades

      MARK - Uma oportunidade para cada intervalo de marcas válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.MARK`

      DELETE - Uma oportunidade para cada intervalo de exclusão válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`

      REPLACE - Duas oportunidades para cada intervalo de substituição válido:

      1. Uma oportunidade de excluir intervalo de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`.

      1. Uma oportunidade de anúncio de decisão do Primetime de `PlacementType.MID_ROLL` ou `PlacementType.PRE_ROLL` e `PlacementMode.FREEREPLACE`

* Adicionado `CustomRangeResolver`:

   * `doCanResolve()` devoluções `true` para excluir intervalos.

   * Adicionado `createDeleteRangeOperation()` para criar `DeleteRange` para a inserção

* Adicionado `CustomRangeHelper`:

   * Classe de utilitário comum para extrair marcar/excluir/substituir `timeRanges` e processá-los.
   * Adicionado `extractCustomRangesMetadata()`
   * Adicionado `extractCustomRanges()`
   * Adicionado `mergeRanges()` - Resolve conflitos e subconjuntos/mesclagens

* `MediaPlayerTimeline`:

   * &quot;>Em `executeOperation()`, se a operação for `DeleteRange`, chamada adicionada para remover o método na operação

   * Entrada `executeOperation()`, se a operação for `NOPTimelineOperation` (vazio) `AdBreaks` retornando do servidor), chamada adicionada para limpar.

   * Adicionado `onDeleteRangeComplete()`
   * Adicionado `removeRange()`
   * Entrada `adjustPlacement()`, para `PlacementMode.FREEREPLACE` , zerou a duração. Essa duração é necessária anteriormente ao solicitar `AdBreaks`, neste ponto precisa ser zero para ser pura inserção.

* `VideoEngineTimeline` Adicionado `removeC3Ad()` - chamar `removeByLocalTime()` para excluir intervalos

* `AdSignalingModeGenerator`

   * `doConfigure()` - Não resolver se nenhuma oportunidade for gerada
   * `createInitialOpportunity()` - Não gerar oportunidade inicial para `AdSignalingMode.CUSTOM_RANGE`. A variável `CustomRangeOpportunityGenerator` já abrange esta questão.

* `DeleteRange`

   * Estende `TimelineOperation`.
   * Criado por `CustomRangeResolver` para exclusão e substituição (a parte de exclusão da substituição)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir embalagem
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` A variável `accepts()` O método foi modificado para permitir a embalagem de tipos diferentes de posicionamento (antes da exibição, durante a exibição, depois da exibição)

* `AuditudeRequestHelper` Correções de erros para permitir a substituição do servidor dos parâmetros Ad

* `AuditudeResolver` A variável `canBePacked()` o método foi alterado para permitir a embalagem

* `CustomAdResolver` A variável `timeRange` as funções de extração foram removidas. Nós obtemos um posicionamento por vez, e transformamos isso em um `AdBreakPlacement timelineOperation`.
