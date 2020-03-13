---
description: Essas alterações no TVSDK suportam exclusão e substituição.
seo-description: Essas alterações no TVSDK suportam exclusão e substituição.
seo-title: Remoção de anúncios e alterações de API de substituição
title: Remoção de anúncios e alterações de API de substituição
uuid: 9d208d3b-6459-4aaf-bc56-53c405ccc1b6
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Remoção de anúncios e alterações de API de substituição {#ad-deletion-and-replacement-api-changes}

Essas alterações no TVSDK suportam exclusão e substituição.

* `AdSignalingMode` Adicionado o modo `CUSTOM_RANGES` de sinalização.

* `OpportunityGenerator`  `extractAdSignalingMode()` - defina `AdSignalingMode.CUSTOM_RANGES` se os intervalos de substituição estão nos metadados.

* `PlacementType` Tipo adicionado `CUSTOM_RANGE` .

* `PlacementMode`

   * Adicionado o `DELETE` modo.
   * Modo adicionado `MARK`
   * Modo adicionado `FreeReplace` - Este modo tem uma duração, mas é uma inserção pura

* `TimeRange` Não é mais uma `final` classe

* Método adicionado `ReplaceTimeRange()`

   Estende-se `TimeRange` para ter uma `replacementDuration` propriedade. Para os casos MARK e DELETE, `replacementDuration` é 0.

* `TimeRangeCollection`

   * Função `toReplaceMetadata()` de utilitário adicionada para extrair `timeRanges`.

   * Modificado para trabalhar com `DELETE` e `REPLACE`

   * `METADATA_KEY_CUSTOM_MARK_RANGES`, `METADATA_KEY_CUSTOM_DELETE_RANGES`, `METADATA_KEY_CUSTOM_REPLACE_RANGES`

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

      * Adicionar `CustomRangeResolver` para quando os intervalos personalizados EXCLUIR e SUBSTITUIR estiverem presentes nos metadados
      * Movido `CustomAdMarkerResolver` antes de `AuditudeResolver`


* Adicionado `CustomRangeOpportunityGenerator`

   * `doUpdate()` Deixa em branco - sem atualização, VOD
   * `doProcess()` Cria uma nova disposição de um novo tipo `Placement.Delete_Range`

   * Adicionados `CustomRangeOppotunityGenerator` à parte superior da lista de geradores em `DefaultContentFactory`, portanto, os intervalos de exclusão são processados antes das inserções de anúncios.

   * Adicionado `createCustomRangeOpportunities` para criar todas as oportunidades

      MARK - uma oportunidade para cada intervalo de marcas válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.MARK`

      EXCLUIR - uma oportunidade para cada intervalo de exclusão válido de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`

      SUBSTITUIR - Duas oportunidades para cada intervalo de substituição válido:

      1. Uma oportunidade de exclusão de intervalo de `PlacementType.CUSTOM_RANGE` e `PlacementMode.DELETE`.

      1. Uma oportunidade de anúncio de decisão Primetime `PlacementType.MID_ROLL` ou `PlacementType.PRE_ROLL` e `PlacementMode.FREEREPLACE`

* Adicionado `CustomRangeResolver`:

   * `doCanResolve()` retorna `true` para intervalos de exclusão.

   * Adicionado `createDeleteRangeOperation()` para criar `DeleteRange` a disposição

* Adicionado `CustomRangeHelper`:

   * Classe de utilitário comum para extrair Mark/Delete/Replace `timeRanges` e processá-los.
   * Adicionado `extractCustomRangesMetadata()`
   * Adicionado `extractCustomRanges()`
   * Adicionado `mergeRanges()` - Resolve conflitos e subconjuntos/mesclagens

* `MediaPlayerTimeline`:

   * &quot;>Em `executeOperation()`, se a operação for `DeleteRange`, foi adicionada uma chamada para remover o método na operação

   * Em `executeOperation()`, se a operação estiver `NOPTimelineOperation` (vazia `AdBreaks` voltando do servidor), foi adicionada uma chamada para limpar.

   * Adicionado `onDeleteRangeComplete()`
   * Adicionado `removeRange()`
   * No modo `adjustPlacement()`, no modo `PlacementMode.FREEREPLACE` , a duração foi zerada. Essa duração é necessária mais cedo ao solicitar `AdBreaks`, nesse ponto, precisa ser zero para ser uma inserção pura.

* `VideoEngineTimeline` Adicionado `removeC3Ad()` - chamada `removeByLocalTime()` para intervalos de exclusão

* `AdSignalingModeGenerator`

   * `doConfigure()` - Não resolver se nenhuma oportunidade for gerada
   * `createInitialOpportunity()` - Não gerar uma oportunidade inicial para `AdSignalingMode.CUSTOM_RANGE`. O `CustomRangeOpportunityGenerator` assunto já está coberto.

* `DeleteRange`

   * Estende-se `TimelineOperation`.
   * Criado `CustomRangeResolver` para exclusão e substituição (a parte de exclusão da substituição)

* `AuditudeConstant`

   * `MAX_PLACEMENTS_PER_REQUEST 1->5` - permitir a embalagem
   * `MINIMUM_AD_DURATION 10->5`

* `AuditudeRequest` O `accepts()` método foi modificado para permitir a embalagem de diferentes tipos de posicionamento (pre-roll, mid-roll, post-roll)

* `AuditudeRequestHelper` Correções de erros para permitir a substituição de parâmetros de anúncio pelo servidor

* `AuditudeResolver` O `canBePacked()` método foi alterado para permitir o empacotamento

* `CustomAdResolver` As funções `timeRange` de extração foram removidas. Nós conseguimos uma disposição de cada vez, e transformamos isso em uma `AdBreakPlacement timelineOperation`.

