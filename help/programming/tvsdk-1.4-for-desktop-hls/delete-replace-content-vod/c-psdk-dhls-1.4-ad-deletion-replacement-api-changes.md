---
description: Essas alterações no TVSDK são compatíveis com exclusão e substituição de anúncios.
title: Exclusão de anúncios e alterações da API de substituição
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---


# Exclusão de anúncio e alterações de substituição da API {#ad-deletion-and-replacement-api-changes}

Essas alterações no TVSDK são compatíveis com exclusão e substituição de anúncios.

* `AdSignalingMode` Adicionado o modo  `CUSTOM_RANGES` de sinalização.

* `OpportunityGenerator`  `extractAdSignalingMode()` - Defina  `AdSignalingMode.CUSTOM_RANGES` se os intervalos de substituição estão nos metadados.

* `PlacementType` Adição  `CUSTOM_RANGE` do tipo .

* `PlacementMode`

   * Adição do modo `DELETE` .
   * Adicionado o modo `MARK`
   * Modo `FreeReplace` adicionado - Esse modo tem uma duração, mas é uma inserção pura

* `TimeRange` Não é mais uma  `final` classe

* Adição do método `ReplaceTimeRange()`

   Estende `TimeRange` para ter uma propriedade `replacementDuration`. Para os casos MARK e DELETE, `replacementDuration` é 0.

* `TimeRangeCollection`

   * Adição da função do utilitário `toReplaceMetadata()` para extrair `timeRanges`.

   * Modificado para trabalhar com `DELETE` e `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`,  `METADATA_KEY_CUSTOM_DELETE_RANGES`,  `METADATA_KEY_CUSTOM_REPLACE_RANGES`

* `CatalogItem`

   * Adição de `createCustomTimeRangesFrom()` - Cria metadados para casos de uso de MARK/DELETE/REPLACE do arquivo JSON.
   * Removido `createCustomAdMarkersMetadataFrom()`

* `DefaultMetadataKeys`

   * Adição de `CUSTOM_DELETE_RANGES_METADATA_KEY`
   * Adição de `CUSTOM_REPLACE_RANGES_METADATA_KEY`
   * `CUSTOM_AD_MARKERS_METADATA_KEY` (não foi alterado)

* `DefaultContentFactory`

   * `doRetrieveGenerators()`

      * Adição de `CustomRangesOpportunityGenerator` para quando os metadados contêm intervalos personalizados
   * `doRetrieveResolvers()`

      * Adicione `CustomRangeResolver` para quando DELETE e os intervalos personalizados REPLACE estiverem presentes nos metadados
      * Movido `CustomAdMarkerResolver` para frente de `AuditudeResolver`


* Adição de `CustomRangeOpportunityGenerator`

   * `doUpdate()` Deixa em branco - sem atualização, VOD
   * `doProcess()` Cria uma nova disposição de um novo tipo  `Placement.Delete_Range`

   * Adição de `CustomRangeOppotunityGenerator` à parte superior da lista de geradores em `DefaultContentFactory`, portanto, os intervalos de exclusão são processados antes da inserção do anúncio.

   * Adição de `createCustomRangeOpportunities` para criar todas as oportunidades

      MARK - Uma oportunidade para cada intervalo de marcas válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.MARK`

      DELETE - Uma oportunidade para cada intervalo de exclusão válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`

      SUBSTITUIR - Duas oportunidades para cada intervalo de substituição válido:

      1. Uma oportunidade de exclusão de intervalo de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`.

      1. Uma oportunidade de anúncio de decisão do Primetime de `PlacementType.MID_ROLL` ou `PlacementType.PRE_ROLL` e `PlacementMode.FREEREPLACE`

* Adição de `CustomRangeResolver`:

   * `doCanResolve()` retorna  `true` para intervalos de exclusão.

   * Adição de `createDeleteRangeOperation()` para criar `DeleteRange` para a disposição

* Adição de `CustomRangeHelper`:

   * Classe de utilitário comum para extrair Mark/Delete/Replace `timeRanges` e processá-los.
   * Adição de `extractCustomRangesMetadata()`
   * Adição de `extractCustomRanges()`
   * `mergeRanges()` adicionado - Resolve conflitos e subconjuntos/mesclagens

* `MediaPlayerTimeline`:

   * &quot;>Em `executeOperation()`, se a operação for `DeleteRange`, foi adicionada uma chamada para remover método na operação

   * Em `executeOperation()`, se a operação for `NOPTimelineOperation` (vazio `AdBreaks` retornando do servidor), adição de chamada para limpar.

   * Adição de `onDeleteRangeComplete()`
   * Adição de `removeRange()`
   * Em `adjustPlacement()`, para o modo `PlacementMode.FREEREPLACE`, a duração foi zerada. Essa duração é necessária anteriormente ao solicitar `AdBreaks`, nesse ponto, precisa ser zero para ser uma inserção pura.

* `VideoEngineTimeline` Adicionado  `removeC3Ad()` - chamada  `removeByLocalTime()` para intervalos de exclusão

* `AdSignalingModeGenerator`

   * `doConfigure()` - Não resolver se nenhuma oportunidade for gerada
   * `createInitialOpportunity()` - Não gerar oportunidade inicial para  `AdSignalingMode.CUSTOM_RANGE`. O `CustomRangeOpportunityGenerator` já cobre isso.

* `DeleteRange`

   * Estende `TimelineOperation`.
   * Criado por `CustomRangeResolver` para exclusão e substituição (a parte de exclusão da substituição)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir a embalagem
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` O  `accepts()` método foi modificado para permitir a embalagem de diferentes tipos de posição (antes da exibição, intermediário, posterior)

* `AuditudeRequestHelper` Correções de erros para permitir a substituição de parâmetros de anúncio pelo servidor

* `AuditudeResolver` O  `canBePacked()` método foi alterado para permitir a embalagem

* `CustomAdResolver` As funções  `timeRange` de extração foram removidas. Obtemos uma disposição de cada vez e transformamos isso em um `AdBreakPlacement timelineOperation`.

