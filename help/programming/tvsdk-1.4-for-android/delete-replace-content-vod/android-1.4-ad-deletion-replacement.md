---
description: Essas alterações na API TVSDK do Android suportam exclusão e substituição.
seo-description: Essas alterações na API TVSDK do Android suportam exclusão e substituição.
seo-title: Remoção de anúncios e alterações de API de substituição
title: Remoção de anúncios e alterações de API de substituição
uuid: 2bb8a331-6851-4442-99de-b01500a0e1e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---


# A exclusão de anúncios e as alterações da API de substituição{#ad-deletion-and-replacement-api-changes}

Essas alterações na API TVSDK do Android suportam exclusão e substituição.

* `AdSignalingMode` Novo Modo Personalizado de Sinalização de Anúncio de Intervalo de Tempo

* `AdvertisingMetadata` Novo  `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: Define os intervalos de tempo para marcar, excluir ou substituir ao processar metadados

* `ContentResolver`

   * Novo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Novo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Nova classe `ContentRemoval`

   `TimelineOperation` classe que define o intervalo de tempo a ser removido da linha do tempo

* `AuditudeResolver`

   * Novo `private LinkedList<AuditudeRequest> _requestQueue`
   * Novo `void startConsumer()`: Start que processam a fila de solicitações de decisão do anúncio Primetime e garantem que cada solicitação seja emitida em intervalos `MIN_INIT_REQUEST_INTERVAL`

   * Novo `processReplacementRange()`: Extrai intervalos de tempo dos metadados do anúncio e gera `PlacementInformations`, além de criar uma solicitação de decisão de anúncio Primetime contendo o `PlacementInformations`.

   * Novo `canDoResolver()`: Verifica se a oportunidade de posicionamento tem metadados de decisão do anúncio Primetime

* Nova classe `CustomRangeHelper` Helper que extrai metadados de intervalo de tempo de metadados de anúncio e remove subconjuntos/sobreposições/intervalos de tempo inválidos.

* Novo `DeleteContentResolver` Resolução de conteúdo que resolve as oportunidades de posicionamento de `PlacementInformation.Mode.DELETE`

* Nova `NopTimelineOperation` nova operação de linha do tempo para quando nenhuma disposição ou substituição de anúncios precisa ser feita. Essa classe é usada para distinguir entre isso e quando ocorre um erro durante o processo de resolução.

* `TimelineOperationQueue` Verifica se a operação da linha do tempo é uma operação  `NopTimelineOperation` antes do processamento.

* `CustomAdMarkersContentResolver` Novo  `canDoResolve()`: Verifica se uma oportunidade de posicionamento é do tipo  `Mode.MARK`

* `MetadataResolver` Novo  `canDoResolve()`: Verifica se uma oportunidade de posicionamento é do tipo  `Mode.INSERT`

* `DefaultMetadataKeys` Novo  `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Novo modo `enum (INSERT, DELETE, REPLACE, MARK)`
   * Novo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Novo  `compareTo(TimeRange timeRange)`: Assim, é possível classificar TimeRanges com base na hora de início

* Novo `ReplacementTimeRange` Estende a classe `TimeRange` que representa um intervalo de tempo de substituição, com um parâmetro `begin`, `end` e `replacement-duration`.

* `TimeRangeCollection`

   * Novo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Renomeado `CUSTOM_AD_MARKERS` para `MARK_RANGES`

   * Modificado `toMetadata(Metadata options)` para colocar os intervalos de exclusão/marca/substituição nos metadados do anúncio.

* `MediaPlayerNotification`

   * Novo `UNDEFINED_TIME_RANGES`: Quando o modo de sinalização de anúncio é Server Map ou Manifest Cue, e os intervalos de substituição também estão nos metadados de anúncio, os intervalos de substituição são ignorados.
   * Novo `REPLACE_RANGES_NOT_AVAILABLE`: Quando o modo de sinalização de anúncio for Intervalos de tempo personalizados e os intervalos de substituição não estiverem disponíveis, um aviso será despachado.

* `AdvertisingFactory` Novo  `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Novo  `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Novo  `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * Em `prepareToPlay()`: Faz uma busca inicial para 0, pois se o intervalo `[0,n]` for excluído, o player de mídia não será reproduzido automaticamente.

   * Em `prepareToPlay()`: Faz loop pela lista de informações iniciais de posicionamento para `mediaplayerclient` resolver.

   * Em `extractAdSignalingMode()`: Acomodar para o novo modo Intervalo de tempo personalizado.
   * Novo `private static List<PlacementInformation> createInitalPlacementInformations()`: Gera as informações iniciais de posicionamento para o modo de sinalização do anúncio e os resolvedores de conteúdo (derivados de metadados do anúncio).
   * Em `ContentPlacementCompletedListener`: Verifica se `mediaPlayerClient` é `doneInitialResolving` antes de chamar `endAdResolving`.

* `MediaPlayerClient`

   * Novo `List<ContentResolver> _contentResolvers`
   * Novo `int _reservations`
   * Novo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: Procura qual resolvedor pode resolver o `PlacementOpportunity`.

   * Código modificado para criar vários resolvedores de conteúdo.
   * Novo `public boolean doneInitialResolving()`: Verifica se há alguma oportunidade a ser resolvida.

* `VideoEngineTimeline`

   * Novo `removeContent(TimelineOperation timelineOperation)`: Remove um determinado intervalo de conteúdo da linha do tempo.
   * Novo `removeContentByLocalTime(long begin, long end)`: Remove o conteúdo de acordo com o horário local especificado `begin` e `end`.

* `DefaultOpportunityDetectorFactory` Modificado  `createOpportunityDetector`: Para fluxos VOD, retorna um novo somente  `SpliceOutOpportunityDetector` se não houver intervalos MARK ou REPLACE (já que esses intervalos têm prioridade sobre o modo de sinalização).

