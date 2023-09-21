---
description: Essas alterações na API TVSDK do Android oferecem suporte à exclusão e substituição de anúncios.
title: Alterações na exclusão de anúncios e na API de substituição
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '428'
ht-degree: 0%

---

# Alterações na exclusão de anúncios e na API de substituição{#ad-deletion-and-replacement-api-changes}

Essas alterações na API TVSDK do Android oferecem suporte à exclusão e substituição de anúncios.

* `AdSignalingMode` Novo modo de sinalização de anúncio de intervalo de tempo personalizado

* `AdvertisingMetadata` Novo `setTimeRanges(TimeRangeCollection timeRanges, Metadata options)`: define os intervalos de tempo para marcar, excluir ou substituir ao processar metadados

* `ContentResolver`

   * Novo `public final boolean canResolve(PlacementOpportunity placementOpportunity)`
   * Novo `protected abstract boolean doCanResolve(PlacementOpportunity placementOpportunity)`

* Novo `ContentRemoval` classe

  `TimelineOperation` classe que define o intervalo de tempo a ser removido da linha do tempo

* `AuditudeResolver`

   * Novo `private LinkedList<AuditudeRequest> _requestQueue`
   * Novo `void startConsumer()`: inicia o processamento da fila de solicitações do Primetime e da decisão e garante que cada solicitação seja emitida em `MIN_INIT_REQUEST_INTERVAL` intervalos

   * Novo `processReplacementRange()`: extrai intervalos de tempo dos metadados de publicidade e gera `PlacementInformations`, e cria uma solicitação do Primetime ad decisioning contendo o `PlacementInformations`.

   * Novo `canDoResolver()`: verifica se a oportunidade de posicionamento tem metadados de Primetime e decisão

* Novo `CustomRangeHelper` Classe auxiliar que extrai metadados de intervalo de tempo dos metadados de anúncio e remove subconjuntos/sobreposições/intervalos de tempo inválidos.

* Novo `DeleteContentResolver` Resolvedor de conteúdo que resolve oportunidades de Posicionamento do `PlacementInformation.Mode.DELETE`

* Novo `NopTimelineOperation` Nova operação de linha do tempo para quando nenhuma inserção ou substituição de ad break precisa ser feita. Essa classe é usada para distinguir entre isso e quando ocorre um erro durante o processo de resolução.

* `TimelineOperationQueue` Verifica se a Operação de Linha do Tempo é `NopTimelineOperation` antes do processamento.

* `CustomAdMarkersContentResolver` Novo `canDoResolve()`: verifica se uma oportunidade de posicionamento é do tipo `Mode.MARK`

* `MetadataResolver` Novo `canDoResolve()`: verifica se uma oportunidade de posicionamento é do tipo `Mode.INSERT`

* `DefaultMetadataKeys` Novo `TIME_RANGES_METADATA_KEY("time_ranges_metadata_key")`

* `PlacementInformation`

   * Novo modo `enum (INSERT, DELETE, REPLACE, MARK)`
   * Novo tipo `CUSTOM_TIME_RANGES`

* `TimeRange` Novo `compareTo(TimeRange timeRange)`: Para classificar intervalos de tempo com base na hora de início

* Novo `ReplacementTimeRange` Estende o `TimeRange` classe que representa um intervalo de tempo de substituição, com um `begin`, `end`, e `replacement-duration` parâmetro.

* `TimeRangeCollection`

   * Novo `MARK_RANGES, DELETE_RANGES, REPLACE_RANGES`
   * Renomeado `CUSTOM_AD_MARKERS` para `MARK_RANGES`

   * Modificado `toMetadata(Metadata options)` para inserir intervalos de exclusão/marcação/substituição nos metadados de anúncios.

* `MediaPlayerNotification`

   * Novo `UNDEFINED_TIME_RANGES`: quando o modo de sinalização de anúncio é Mapa do servidor ou Indicações de manifesto e os intervalos de substituição também estão nos metadados de anúncio, os intervalos de substituição são ignorados.
   * Novo `REPLACE_RANGES_NOT_AVAILABLE`: quando o modo de sinalização de anúncio for Intervalos de tempo personalizados e os intervalos de substituição não estiverem disponíveis, um aviso será despachado.

* `AdvertisingFactory` Novo `public abstract List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultAdvertisingFactory` Novo `public List<ContentResolver> createContentResolvers(MediaPlayerItem item)`

* `DefaultContentResolverFactory` Novo `public static List<ContentResolver> createContentResolvers(MediaResource resource, Context context)`

* `DefaultMediaPlayer`

   * Entrada `prepareToPlay()`: faz uma busca inicial até 0, porque se o intervalo `[0,n]` for excluído, o reprodutor de mídia não será reproduzido automaticamente.

   * Entrada `prepareToPlay()`: Executa um loop pela lista de informações de posicionamento inicial para `mediaplayerclient` para resolver.

   * Entrada `extractAdSignalingMode()`: acomode para o novo modo Intervalo de tempo personalizado.
   * Novo `private static List<PlacementInformation> createInitalPlacementInformations()`: gera as informações de posicionamento inicial para o modo de sinalização de anúncio e os resolvedores de conteúdo (derivados dos metadados de anúncio).
   * Entrada `ContentPlacementCompletedListener`: verifica se `mediaPlayerClient` é `doneInitialResolving` antes de chamar `endAdResolving`.

* `MediaPlayerClient`

   * Novo `List<ContentResolver> _contentResolvers`
   * Novo `int _reservations`
   * Novo `lookupContentResolver(PlacementOpportunity placementOpportunity)`: verifica qual resolvedor pode resolver o `PlacementOpportunity`.

   * Código modificado para criar vários resolvedores de conteúdo.
   * Novo `public boolean doneInitialResolving()`: verifica se há oportunidades a serem resolvidas.

* `VideoEngineTimeline`

   * Novo `removeContent(TimelineOperation timelineOperation)`: remove um determinado intervalo de conteúdo da linha do tempo.
   * Novo `removeContentByLocalTime(long begin, long end)`: remove o conteúdo por hora local `begin` e `end`.

* `DefaultOpportunityDetectorFactory` Modificado `createOpportunityDetector`: para fluxos de VOD, retorne apenas um novo `SpliceOutOpportunityDetector` se não houver intervalos MARK ou REPLACE (já que esses intervalos têm prioridade sobre o modo de sinalização).
