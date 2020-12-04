---
description: Essas alterações no TVSDK suportam exclusão e substituição.
seo-description: Essas alterações no TVSDK suportam exclusão e substituição.
seo-title: Remoção de anúncios e alterações de API de substituição
title: Remoção de anúncios e alterações de API de substituição
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---


# A exclusão de anúncios e as alterações de API de substituição {#ad-deletion-and-replacement-api-changes}

Essas alterações no TVSDK suportam exclusão e substituição.

* `AdSignalingMode` Adicionado o modo  `CUSTOM_RANGES` de sinalização.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Defina  `AdSignalingMode.CUSTOM_RANGES` se os intervalos de substituição estão nos metadados.

* `PlacementType` Adicionado o  `CUSTOM_RANGE` tipo.

* `PlacementMode`

   * Adicionado o modo `DELETE`.
   * Adicionado o modo `MARK`
   * Adicionado o modo `FreeReplace` - Este modo tem uma duração, mas é uma inserção pura

* `TimeRange` Não é mais uma  `final` classe

* Método `ReplaceTimeRange()` adicionado

   Estende `TimeRange` para ter uma propriedade `replacementDuration`. Para os casos MARK e DELETE, `replacementDuration` é 0.

* `TimeRangeCollection`

   * Adição da função de utilitário `toReplaceMetadata()` para extrair `timeRanges`.

   * Modificado para trabalhar com `DELETE` e `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`,  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Adicionado `createCustomTimeRangesFrom()` - cria metadados para casos de uso MARK/DELETE/REPLACE a partir do arquivo JSON.
   * Removido `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Adicionado `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Adicionado `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (não foi alterado)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Adicionado `CustomRangesOpportunityGenerator` para quando os metadados contêm intervalos personalizados
   * `doRetrieveResolvers()`

      * Adicione `CustomRangeResolver` para quando DELETE e REPLACE estiverem presentes intervalos personalizados nos metadados
      * Movido `CustomAdMarkerResolver` para frente de `AuditudeResolver`


* Adicionado `CustomRangeOpportunityGenerator`

   * `doUpdate()` Deixa em branco - sem atualização, VOD
   * `doProcess()` Cria uma nova disposição de um novo tipo  `Placement.Delete_Range`

   * Adicionados `CustomRangeOppotunityGenerator` à parte superior da lista de geradores em `DefaultContentFactory`, portanto, os intervalos de exclusão são processados antes das inserções de anúncios.

   * Adicionado `createCustomRangeOpportunities` para criar todas as oportunidades

      MARK - uma oportunidade para cada intervalo de marcas válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.MARK`

      DELETE - Uma oportunidade para cada intervalo de exclusão válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`

      SUBSTITUIR - Duas oportunidades para cada intervalo de substituição válido:

      1. Uma oportunidade de exclusão de intervalo de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`.

      1. Uma oportunidade de anúncio de decisão Primetime de `PlacementType.MID_ROLL` ou `PlacementType.PRE_ROLL` e `PlacementMode.FREEREPLACE`

* Adicionado `CustomRangeResolver`:

   * `doCanResolve()` retorna  `true` para intervalos de exclusão.

   * Adicionado `createDeleteRangeOperation()` para criar `DeleteRange` para a disposição

* Adicionado `CustomRangeHelper`:

   * Classe de utilitário comum para extrair Mark/Delete/Replace `timeRanges` e processá-los.
   * Adicionado `extractCustomRangesMetadata()`
   * Adicionado `extractCustomRanges()`
   * Adicionado `mergeRanges()` - Resolve conflitos e subconjuntos/mesclagens

* `MediaPlayerTimeline`:

   * &quot;>Em `executeOperation()`, se a operação for `DeleteRange`, foi adicionada uma chamada para remover o método na operação

   * Em `executeOperation()`, se a operação for `NOPTimelineOperation` (vazia `AdBreaks` voltando do servidor), foi adicionada uma chamada para limpar.

   * Adicionado `onDeleteRangeComplete()`
   * Adicionado `removeRange()`
   * No modo `adjustPlacement()`, para `PlacementMode.FREEREPLACE`, a duração foi zerada. Essa duração é necessária mais cedo ao solicitar `AdBreaks`, nesse ponto, precisa ser zero para ser uma inserção pura.

* `VideoEngineTimeline` Adicionada  `removeC3Ad()` - chamada  `removeByLocalTime()` para intervalos de exclusão

* `AdSignalingModeGenerator`

   * `doConfigure()` - Não resolver se nenhuma oportunidade for gerada
   * `createInitialOpportunity()` - Não gerar uma oportunidade inicial para  `AdSignalingMode.CUSTOM_RANGE`. O `CustomRangeOpportunityGenerator` já cobre isso.

* `DeleteRange`

   * Estende `TimelineOperation`.
   * Criado por `CustomRangeResolver` para exclusão e substituição (a parte de exclusão da substituição)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir a embalagem
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` O  `accepts()` método foi modificado para permitir a embalagem de diferentes tipos de posicionamento (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correções de erros para permitir a substituição de parâmetros de anúncio pelo servidor

* `AuditudeResolver` O  `canBePacked()` método foi alterado para permitir o empacotamento

* `CustomAdResolver` As funções de  `timeRange` extração foram removidas. Obtemos uma disposição de cada vez e transformamos isso em um `AdBreakPlacement timelineOperation`.

