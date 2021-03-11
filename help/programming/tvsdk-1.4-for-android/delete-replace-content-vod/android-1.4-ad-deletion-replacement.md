---
description: Essas alterações na API TVSDK do Android são compatíveis com exclusão e substituição de anúncios.
title: Exclusão de anúncios e alterações da API de substituição
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---


# A exclusão de anúncios e as alterações de substituição da API{#ad-deletion-and-replacement-api-changes}

Essas alterações na API TVSDK do Android são compatíveis com exclusão e substituição de anúncios.

* `AdSignalingMode` Novo modo de sinalização de anúncio de intervalo de tempo personalizado

* `AdvertisingMetadata` Novo  `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Define os intervalos de tempo para marcar, excluir ou substituir durante o processamento de metadados

* `ContentResolver`

   * Novo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Novo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nova classe `ContentRemoval`

   `TimelineOperation` classe que define o intervalo de tempo a ser removido da linha do tempo

* `AuditudeResolver`

   * Novo `private LinkedList<AuditudeRequest> _requestQueue`
   * Novo `void startConsumer()`: Inicia o processamento da fila de solicitações de decisão do Primetime e garante que cada solicitação seja emitida em intervalos `MIN_INIT_REQUEST_INTERVAL`

   * Novo `processReplacementRange()`: Extrai intervalos de tempo dos metadados do anúncio e gera `PlacementInformations`, além de criar uma solicitação de decisão de anúncio do Primetime contendo o `PlacementInformations`.

   * Novo `canDoResolver()`: Verifica se a oportunidade de posicionamento tem metadados de decisão do anúncio do Primetime

* Nova `CustomRangeHelper` classe de ajuda que extrai metadados de intervalo de tempo de metadados de anúncios e remove subconjuntos/sobreposições/intervalos de tempo inválidos.

* Novo `DeleteContentResolver` Resolvedor de conteúdo que resolve as oportunidades de posicionamento de `PlacementInformation.Mode.DELETE`

* Nova `NopTimelineOperation` nova operação de linha do tempo para quando nenhuma disposição ou substituição de ad break precisa ser feita. Essa classe é usada para distinguir entre isso e quando ocorre um erro durante o processo de resolução.

* `TimelineOperationQueue` Verifica se a Operação da Linha do Tempo é uma operação  `NopTimelineOperation` antes do processamento.

* `CustomAdMarkersContentResolver` Novo  `canDoResolve()`: Verifica se uma oportunidade de posicionamento é do tipo  `Mode.MARK`

* `MetadataResolver` Novo  `canDoResolve()`: Verifica se uma oportunidade de posicionamento é do tipo  `Mode.INSERT`

* `DefaultMetadataKeys` Novo  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Novo modo `enum (INSERT, DELETE, REPLACE, MARK)`
   * Novo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Novo  `compareTo(TimeRange timeRange)`: Assim, você pode classificar os Intervalos de tempo com base no horário de início

* Novo `ReplacementTimeRange` Estende a classe `TimeRange` que representa um intervalo de tempo de substituição, com um parâmetro `begin`, `end` e `replacement-duration`.

* `TimeRangeCollection`

   * Novo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * `CUSTOM_AD_MARKERS` renomeado para `MARK_RANGES`

   * Modificado `toMetadata(Metadata options)` para colocar os intervalos de exclusão/marca/substituição em metadados de anúncio.

* `MediaPlayerNotification`

   * Novo `UNDEFINED_TIME_RANGES`: Quando o modo de sinalização do anúncio é Mapa do servidor ou Casos de manifesto e os intervalos de substituição também estão nos metadados do anúncio, os intervalos de substituição são ignorados.
   * Novo `REPLACE_RANGES_NOT_AVAILABLE`: Quando o modo de sinalização do anúncio for Personalizar intervalos de tempo e os intervalos de substituição não estiverem disponíveis, um aviso será despachado.

* `AdvertisingFactory` Novo  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Novo  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Novo  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * Em `prepareToPlay()`: Faz uma busca inicial para 0, porque se o intervalo `[0,n]` for excluído, o reprodutor de mídia não será reproduzido automaticamente.

   * Em `prepareToPlay()`: Faz o loop pela lista de informações de posicionamento inicial para `mediaplayerclient` resolver.

   * Em `extractAdSignalingMode()`: Acomodar para o novo modo Intervalo de tempo personalizado.
   * Novo `private static List<PlacementInformation> createInitalPlacementInformations()`: Gera as informações de posicionamento inicial para o modo de sinalização de anúncios e os resolvedores de conteúdo (derivados de metadados de anúncios).
   * Em `ContentPlacementCompletedListener`: Verifica se `mediaPlayerClient` é `doneInitialResolving` antes de chamar `endAdResolving`.

* `MediaPlayerClient`

   * Novo `List<ContentResolver> _contentResolvers`
   * Novo `int _reservations`
   * Novo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Procura qual resolvedor pode resolver o `PlacementOpportunity`.

   * Código modificado para criar vários resolvedores de conteúdo.
   * Novo `public boolean doneInitialResolving()`: Verifica se há oportunidades restantes para serem resolvidas.

* `VideoEngineTimeline`

   * Novo `removeContent(TimelineOperation timelineOperation)`: Remove um determinado intervalo de conteúdo da linha do tempo.
   * Novo `removeContentByLocalTime(long begin, long end)`: Remove o conteúdo por hora local, considerando `begin` e `end`.

* `DefaultOpportunityDetectorFactory` Modificado  `createOpportunityDetector`: Para fluxos VOD, retorne um novo somente  `SpliceOutOpportunityDetector` se não houver intervalos MARK ou REPLACE (já que esses intervalos têm prioridade sobre o modo de sinalização).

