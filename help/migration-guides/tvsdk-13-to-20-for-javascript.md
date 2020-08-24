---
title: Conversão TVSDK - 1.3 para 2.0 para JavaScript
seo-title: Conversão TVSDK - 1.3 para 2.0 para JavaScript
description: Muitas assinaturas de métodos e nomes de elementos de API foram alterados para 2.0. Revise essas tabelas para ver todos os detalhes de alteração da API.
seo-description: Muitas assinaturas de métodos e nomes de elementos de API foram alterados para 2.0. Revise essas tabelas para ver todos os detalhes de alteração da API.
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: cfd6da49e85e13e29e8458ee98231a8b476867db
workflow-type: tm+mt
source-wordcount: '5058'
ht-degree: 0%

---


# Conversão TVSDK - 1.3 para 2.0 para JavaScript {#tvsdk-conversion-to-for-javascript}

Muitas assinaturas de métodos e nomes de elementos de API foram alterados para 2.0. Revise essas tabelas para ver todos os detalhes de alteração da API.

## Implementar funções de retorno de chamada no JavaScript {#implement-callback-functions-in-javascript}

Os comentários na documentação do método sugerem a assinatura para retornos de chamada que você precisa implementar.

Para JavaScript, a sintaxe da API se baseia na ID da Web. Para uma interface TVSDK, os nomes do método são chamados de *methodName*(). Para que os métodos sejam implementados pelo aplicativo, um atributo de leitura/gravação chamado ** methodNameCallbackFunc é adicionado à interface e seu aplicativo deve defini-lo para apontar para uma função que implementa o método. Por exemplo:

```shell
// An app implementable interface
interface ContentFactory
{
    /*
     * AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item);
     */
    attribute Object retrieveAdPolicySelectorCallbackFunc;
 
    /*
     * ContentResolverList retrieveResolvers(MediaPlayerItem item);
     */
    attribute Object retrieveResolversCallbackFunc;
 
    /*
     * OpportunityGeneratorList retrieveGenerators(MediaPlayerItem item);
     */
    attribute Object retrieveGeneratorsCallbackFunc;
};

// this is how to implement it
var factory = new AdobePSDK.ContentFactory();
factory.retrieveAdPolicySelectorCallbackFunc = function(item)
{
    // return your adPolicySelector according to the item
    return adPolicySelector;
}
 
mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig ();
playerConfig.adFactory = factory;
// Use this config to load new MediaResource
```

## Alterações de elementos da API de fluxo de trabalho de publicidade para 2.0 {#advertising-workflow-api-element-changes-for}

Essas tabelas comparam os elementos da API de fluxo de trabalho de publicidade para o JavaScript TVSDK entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Posicionamento
* Oportunidade
* Reserva
* Linha do tempo / Item da linha do tempo / Marcador da linha do tempo
* AdBreak
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* TimelineOperation
* AdBreakPlacement
* AuditudeSettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>: interface TimedMetadata {<br /> const short METADATA_TYPE_TAG = 0 ; <br /> const short METADATA_TYPE_ID3 não assinado = 1 ; <br /> tipo abreviado não assinado do atributo readonly; <br /> Atributo somente leitura por muito tempo;<br /> atributo readonly DomString id;<br /> atributo readonly nome DomString;<br /> atributo readonly de conteúdo DomString; <br /> Metadados do objeto do atributo readonly;<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const short METADATA_TYPE_TAG = 0 ;<br /> const short METADATA_TYPE_ID3 não assinado = 1 ;<br /> Atributo readonly attribute short metadataType não assinado;<br /> Atributo somente leitura por muito tempo;<br /> id longa do atributo readonly;<br /> atributo readonly nome DomString;<br /> <br /> Metadados do objeto do atributo readonly;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> atributo readonly long length não assinado;<br /> getter TimedMetadata (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSignalingMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interface AdSignalingMode { <br /> const short MODE_DEFAULT não assinado, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const short MODE_SERVER_MAP não assinado, <br /> const short MODE_CUSTOM_RANGES <br /> } não assinado;</p> </td> 
   <td>Isso substitui a chave MetadataKeys::MANIFEST_CUES.</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMetadata {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interface AdvertisingMetadata { <br /> atributo AdSignalingMode mode; <br /> Atributo AdBreakWatchedPolicy adBreakAsWatched; <br /> atributo boolean livePreroll; <br /> attribute boolean delayAdLoading ; <br /> };</p> </td> 
   <td>Esta funcionalidade foi fornecida por<p>MetadataKeys::ADVERTISING_METADATA</p> key.</td> 
  </tr> 
 </tbody> 
</table>

### CustomRangeMetadata {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interface CustomRangeMetadata { <br /> const short TYPE_MARK_RANGE não assinado; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> tipo abreviado não assinado; <br /> Atributo boolean adjustSeekPosition; <br /> atributo TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### ReplaceTimeRange {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface ReplaceTimeRange { <br /> atributo long begin unsigned; <br /> atributo readonly long end não assinado; <br /> Atributo de longa duração não assinado; <br /> Atributo long replaceDuration unsigned; <br /> };</p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Posicionamento {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Posicionamento da interface { <br /> const short não assinado TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> tipo abreviado não assinado do atributo readonly; <br /> Atributo somente leitura por muito tempo; <br /> atributo readonly de longa duração; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const short MODE_MARK não assinado; <br /> const unsigned short MODE_FREE_REPLACE; <br /> Atributo readonly modo abreviado não assinado; <br /> atributo readonly intervalo TimeRange; <br /> };</p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Oportunidade {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>oportunidade de interface { <br /> atributo somente leitura ID de DomString; <br /> colocação do atributo somente leitura; <br /> configurações de Objeto do atributo somente leitura; <br /> atributo readonly object customParameters; <br /> }; </p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Reserva {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>reserva de interface { <br /> atributo somente leitura Intervalo de tempo; <br /> Atribuir somente leitura longa retenção; <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### Linha do tempo / Item da linha do tempo / Marcador da linha do tempo {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p><strong>Linha do tempo</strong>: linha do tempo da interface <br /> { atributo somente leitura TimelineMarkerList timelineMarkers; <br /> atributo readonly TimelineItemList timelineItems; <br /> duplo convertToLocalTime( hora do duplo); <br /> duplo convertToVirtualTime (hora do duplo); <br /> };</p> </td> 
   <td><p>linha do tempo da interface {<br /> atributo somente leitura TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>Item</strong>da linha do tempo: linha do tempo da interfaceItem :<br /> ID longa do atributo somente leitura {<br /> TimelineMarker; <br /> atributo readonly TimeRange virtualRange; <br /> atributo readonly TimeRange localRange; <br /> atributo readonly boolean assistido; <br /> atributo readonly booliano temporário; <br /> }; </p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>MarcadorLinha</strong>do tempo: (Sem alteração para 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> hora do duplo do atributo somente leitura;<br /> duração do duplo do atributo readonly;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdBreak {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreak {<br /> } duração do duplo do atributo somente leitura <br /><br /> <br /> ;<br /> Atributo somente leitura anúncios AdList;<br /> <br /> <br /> atributo readonly AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> hora do duplo do atributo somente leitura;<br /> duplo de atributo readonly replaceDuration;<br /> <br /> duração do duplo do atributo readonly;<br /> atributo readonly AdList adList;<br /> <br /> Atributo somente leitura Dados DomString;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Anúncio</strong>: interface Ad {<br /> atributo somente leitura AdAsset PrimaryAsset;<br /> atributo readonly AdAssetList companionAssets;<br /> <br /> duração do duplo do atributo readonly;<br /> atributo readonly DomString id;<br /> const abreviado não assinado ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> atributo readonly não assinado short adType;<br /> atributo readonly AdInsertionType adInsertionType; <br /> <br /> atributo readonly booleano clicável; <br /> o atributo readonly boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {<br /> atributo somente leitura AdAsset PrimaryAsset;<br /> atributo readonly AdAssetList companionAssets;<br /> <br /> duração do duplo do atributo readonly;<br /> atributo readonly DomString id;<br /> const abreviado não assinado ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINEAR = 1 ;<br /> <br /> tipo abreviado não assinado do atributo readonly;<br /> atributo readonly AdInsertionType insertionType; <br /> Atributo somente leitura Rastreador de objetos;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdAsset {<br /> atributo somente leitura ID DomString;<br /> duração do duplo do atributo readonly;<br /> atributo readonly MediaResource;<br /> atributo somente leitura AdClick adClick;<br /> Metadados do objeto do atributo readonly;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdClick {<br /> atributo somente leitura ID DomString;<br /> atributo readonly título DomString;<br /> atributo readonly url DomString;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdList {<br /> atributo readonly unsigned long length;<br /> getter Ad(índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdAssetList {<br /> atributo readonly long length não assinado;<br /> getter AdAsset (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interface AdBannerAsset: AdAsset<br /> {<br /> atributo somente leitura na largura;<br /> atributo readonly int int height;<br /> atributo readonly DomString staticUrl;<br /> atributo readonly de altura DomString;<br /> Atributo somente leitura Largura DomString;<br /> };</p> </td> 
   <td> Novo no 2.0</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem / AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : Item da linha do tempo { <br /> atributo somente leitura AdBreak adBreak; <br /> itens AdTimelineItemList do atributo readonly; <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : Item da linha do tempo { <br /> atributo somente leitura AdBreak adBreak; <br /> atributo somente leitura Anúncio; <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { <br /> atributo readonly unsigned long length; <br /> getter AdBreakTimelineItem (índice ng não assinado); <br /> };</p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPolicy {<br /> atributo readonly short AD_BREAK_POLICY_SKIP;<br /> atributo readonly short AD_BREAK_POLICY_PLAY;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> atributo readonly short AD_BREAK_POLICY_SKIP;<br /> atributo readonly short AD_BREAK_POLICY_PLAY;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE;<br /> atributo readonly abreviado AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> atributo readonly short AD_POLICY_PLAY;<br /> atributo readonly abreviado AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; atributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> atributo readonly short AD_POLICY_PLAY;<br /> atributo readonly abreviado AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> atributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> atributo readonly short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {atributo readonly short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> atributo somente leitura AdTimelineItem adTimelineItem;<br /> duplo do atributo readonly currentTime;<br /> atributo readonly requestToTime do duplo;<br /> taxa de duplo do atributo readonly;<br /> modo abreviado do atributo readonly; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakPlacementList <br /> adBreakPlacements;<br /> atributo somente leitura Anúncio;<br /> duplo do atributo readonly currentTime;<br /> atributo readonly requestToTime do duplo;<br /> taxa de duplo do atributo readonly;<br /> modo abreviado do atributo readonly; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute Object selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimelineOperation {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>linha do tempo da interfaceOperação { <br /> posicionamento do atributo somente leitura ; <br /> };</p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPlacement {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPlacement: Linha do tempoOperação {<br /> atributo somente leitura AdBreak adBreak;<br /> colocação do atributo somente leitura; // Da Linha do tempoA operação<br /> só de leitura atribui a hora do duplo;<br /> duração do duplo do atributo readonly;<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> atributo somente leitura AdBreak adBreak;<br /> colocação do atributo somente leitura;<br /> tempo de duplo do atributo readonly;<br /> duração do duplo do atributo readonly;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AuditudeSettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AuditudeSettings: AdvertisingMetadata { <br /> atributo DomString zoneId; <br /> Atributo DomString mediaId; <br /> attribute DomString defaultMediaId ; <br /> domínio DomString do atributo ; <br /> attribute Object targettingInfo ; <br /> attribute Object customParameters ; <br /> atributo Boolean creativePackaingEnabled ;<br /> atributo Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>A funcionalidade foi fornecida pela chave MetadataKeys::AUDITUDE_METADATA_KEY.</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API de personalização para 2.0 {#customization-api-element-changes-for}

Essas tabelas comparam os elementos da API de personalização para o JavaScript TVSDK entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> Atributo StringList subscribeTags;<br /> <br /> atributo StringList adTags;<br /> <br /> <br /> Atribua AdSignalingMode adSignalingMode;<br /> atributo CustomRangeMetadata customRangeMetadata;<br /> Atribuir NetworkConfiguration networkConfiguration;<br /> Atributo AdvertisingMetadata advertiadataMetadata;<br /> Atributo Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /><br /> atributo StringList adTags de <br /> <br /> atributo StringList;<br /> Atributo StringList signedTags;<br /> Atribuir MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * item MediaPlayerItem);<br /> */<br /> attribute Object retrieveAdPolicySeletorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * item MediaPlayerItem);<br /> */<br /> attribute Object retrieveAdPolicySeletorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> attribute boolean forceNativeNetworking;<br /> atributo boolean useRedirectUrl;<br /> attribute Object cookieHeader;<br /> atributo boolean readSetCookieHeader;<br /> atributo int masterUpdateInterval; <br /> atributo boolean useCookieHeaderForAllRequests;<br /> attribute int readLimit;<br /> };</p> </td> 
   <td>No 1.3, parte dessa funcionalidade foi fornecida pelo MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API DRM para 2.0 {#drm-api-element-changes-for}

Essas tabelas comparam os elementos da API DRM para o JavaScript TVSDK entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* Inicialização do fluxo de trabalho DRM
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* Política de DRMP
* DRMManager

### Inicialização do fluxo de trabalho DRM {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>O aplicativo precisa chamar o AdobePSDK.initiDRMWorkflow para iniciar o fluxo de trabalho do DRM. Sem esta chamada, os vídeos DRM não serão reproduzidos.<p>interface do AdobePSDK<br /> {<br /> void launchDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>A inicialização foi feita internamente e nenhuma chamada explícita foi necessária.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| APIs 2.0 | 1.3 APIs |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Nenhuma alteração para 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| Nenhuma alteração para 2.0. | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0.</td> 
   <td><p>interface DRMMetadata<br /> {<br /> atributo somente leitura DomString serverUrl;<br /> atributo readonly DomString licenseId;<br /> Atributo readonly às políticas DRMPolicyArray; <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo readonly em playbackPeriodInSeconds;<br /> Atribui somente leitura a playback longStartDate;<br /> Atribui somente leitura a playbackEndDate longa;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo readonly em periodInSeconds;<br /> atributo readonly em startDate;<br /> atributo readonly int em endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0.</td> 
   <td><p>interface DRMLicense {<br /> atributo somente leitura Bytes Uint8Array;<br /> atributo readonly Date licenseStartDate;<br /> atributo readonly Date licenseEndDate;<br /> atributo readonly Date offlineStorageStartDate;<br /> atributo readonly Date offlineStorageEndDate; <br /> atributo readonly DomString serverUrl;<br /> atributo readonly DomString licenseID;<br /> atributo readonly DomString policyID;<br /> atributo readonly DRMPlaybackTimeWindow playbackTimeWindow;<br /> atributo readonly object customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMLicenseDomain {<br /> atributo readonly DomString authenticationDomain;<br /> atributo readonly DRMAuthenticationMethod authenticationMethod; <br /> atributo readonly DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> atributo somente leitura DomString authDomain;<br /> atributo readonly DRMAuthenticationMethod authMethod; <br /> atributo readonly DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Política de DRMP {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPolicy<br /> {<br /> atributo readonly DomString authenticationDomain;<br /> atributo readonly DRMAuthenticationMethod authenticationMethod;<br /> <br /> atributo readonly DomString displayName;<br /> atributo readonly DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {<br /> atributo somente leitura DomString authDomain;<br /> atributo readonly DRMAuthenticationMethod authMethod;<br /> atributo readonly DomString dispName;<br /> atributo readonly DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMManager: EventTarget {<br /> void acquisitionLicense(metadados DRMMetadata, configuração <br /> DRMAcquireLicenseSettings, ouvinte <br /> DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense (metadados DRMMetadata, ouvinte <br /> DRMAquireLicenseListener);<br /> void authenticate(metadados DRMMetadata, url DomString, <br /> DomString &amp;authenticationDomain, usuário<br /> DomString, senha <br /> DomString, ouvinte <br /> <br /> DRMAuthenticateListener);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> matriz Uint8Array, ouvinte DRMErrorListener);<br /> void initialize(ouvinte DRMOperationCompleteListener);<br /> Atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, ouvinte <br /> DRMOperationCompleteListener);<br /> void LeaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, ouvinte <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener listener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> boolean commitImediatamente,<br /> ouvinte DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> metadados DRMMetadata, <br /> DomString authenticationDomain, token <br /> <br /> Uint8Array, ouvinte DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, ouvinte DRMOperationCompleteListener); <br /><br /> };</p> </td> 
   <td><p>interface DRMManager: EventTarget {<br /> void acquisitionLicense(metadados DRMMetadata, configuração <br /> DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreviewLicense (metadados DRMMetadata, <br /> EventContext eventContext);<br /> void authenticate(metadados DRMMetadata, url DomString, <br /> DomString &amp;authenticationDomain, usuário<br /> DomString, senha <br /> DomString, eventContext <br /> <br /> Event);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> matriz Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> Atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> void LeaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> boolean commitImediatamente,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> Metadados DRMMetadata, <br /> DomString authenticationDomain, token <br /> Uint8Array, <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMErrorListener: <br /> psdkutils públicos::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protegido:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando um erro ocorre durante um dos métodos assíncronos do DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMOperationCompleteListener: <br /> public DRMErrorListener {<br /> public:<br /> Virtual void onDRMOperationComplete() = 0;<br /> <br /> protegido:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEEvent</p> <p>Quando a inicialização do DRM estiver concluída.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEEvent</p> <p>Quando a ação joinLicenseDomain() for concluída com êxito.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEEvent</p> <p>Quando a ação LeaveLicenseDomain() for concluída com êxito.</p> </li> 
     <li>kEventDRMResetCompletePSDKEEvent<p>/ PSDKEEvent</p> <p>Quando a ação resetDRM() é concluída com êxito.</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEEvent</p> <p>Quando a ação setAuthenticationTokenSet() é concluída com êxito.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEEvent</p> <p>Quando a ação storeLicenseBytes() é concluída com êxito.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAuthenticateListener: <br /> public DRMErrorListener {<br /> public:<br /> void virtual onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Quando a chamada de método DRMManager::authenticate for bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> Virtual void onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionPreviewLicense for bem-sucedida.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionLicense for bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturn ) = 0;<br /> <br /> protegido:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Quando a chamada do método DRMManager::returnLicense for bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Alterações genéricas de elementos da API de reprodução para 2.0 {#generic-playback-api-element-changes-for}

Essas tabelas comparam os elementos genéricos da API de reprodução entre o JavaScript TVSDK 1.3 e 2.0.

Tabelas neste tópico:

* MediaResource
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> attribute DomString url; <br /> tipo abreviado não assinado;<br /> Metadados do objeto do atributo;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> attribute DomString url;<br /> tipo DomString do atributo;<br /> Metadados do objeto do atributo;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay (posição do duplo);<br /> void play();<br /> void pause();<br /> void search( posição de duplo);<br /> void searchToLocal( posição do duplo);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(item MediaPlayerItem);<br /> void replaceCurrentResource(MediaResource, <br /> MediaPlayerItemConfig); <br /> void drop();<br /> void restore();<br /> void notificationClick();<br /> <br /> atributo readonly TimeRange playbackRange;<br /> atributo readonly TimeRange buskableRange;<br /> duplo do atributo readonly currentTime;<br /> Atributo readonly duplo localTime;<br /> atributo readonly TimeRange bufferedRange;<br /> atributo readonly DRMManager drmManager;<br /> atributo readonly MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> const <br /> <br /> unsigned short PLAYER_STATUS_INITIALIZED;<br /> const short PLAYER_STATUS_PREPARING não assinado;<br /> const short PLAYER_STATUS_PREPARED não assinado;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const short PLAYER_STATUS_SEEKING não assinado;<br /> const short PLAYER_STATUS_COMPLETE não assinado;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> Atributo readonly status abreviado não assinado;<br /> <br /> Atribuir um volume curto não assinado;<br /> Atribuir ABRControlParameters abrControlParameters;<br /> Atributo BufferControlParameters bufferControlParameters;<br /> <br /> const. curta VISÍVEL não assinado; //Para visibilidade<br /> CC const. curta não assinada INVISÍVEL; /For CC atributo de visibilidade<br /> ccVisibility abreviada não assinada;<br /> atributo TextFormat ccStyle;<br /> atributo readonly PlaybackMetrics playbackMetrics;<br /> <br /> taxa de duplo do atributo;<br /> Atribuir visualização MediaPlayerView;<br /> linha do tempo do atributo somente leitura;<br /> duplo de atributo currentTimeUpdateInterval; <br /> // definir isso não será suportado para 2.0<br /> };</p> </td> 
   <td><p>interface MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay( posição int);<br /> void play();<br /> void pause();<br /> void search( int position);<br /> void requestToLocalTime( posição int);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(fonte MediaResource);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo readonly TimeRange playbackRange;<br /> atributo readonly TimeRange buskableRange;<br /> duplo do atributo readonly currentTime;<br /> Atributo readonly duplo localTime;<br /> atributo readonly TimeRange bufferedRange;<br /> atributo readonly DRMManager drmManager;<br /> atributo readonly MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const short não assinado PLAYER_STATE_IDLE;<br /> const short PLAYER_STATE_INITIALIZING não assinado;<br /> const short PLAYER_STATE_INITIALIZED não assinado;<br /> const short PLAYER_STATE_PREPARING não assinado;<br /> const short PLAYER_STATE_PREPARED não assinado;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const short PLAYER_STATE_SEEKING não assinado;<br /> const short PLAYER_STATE_COMPLETE não assinado;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED não assinado;<br /> Atributo somente leitura de estado abreviado não assinado;<br /> <br /> Atribuir um volume curto não assinado;<br /> Atribuir ABRControlParameters abrControlParameters;<br /> Atributo BufferControlParameters bufferControlParameters;<br /> <br /> VISÍVEL curto não assinado; //For CC Visibilidade<br /> somente leitura não assinada curta INVISÍVEL; /For CC atributo de visibilidade<br /> ccVisibility abreviada não assinada;<br /> atributo TextFormat ccStyle;<br /> atributo readonly PlaybackMetrics playbackMetrics;<br /> Atribuir MediaPlayerConfig mediaPlayerConfig;<br /> taxa de duplo do atributo;<br /> Atribuir visualização MediaPlayerView;<br /> linha do tempo do atributo somente leitura;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const short PLAYER_STATUS_IDLE não assinado;<br /> const short PLAYER_STATUS_INITIALIZING não assinado;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const short PLAYER_STATUS_PREPARING não assinado;<br /> const short PLAYER_STATUS_PREPARED não assinado;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const short PLAYER_STATUS_SEEKING não assinado;<br /> const short PLAYER_STATUS_COMPLETE não assinado;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED não assinado;<br /> };</p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Eventos suportados pelo MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>Nome do Evento 2.0</th> 
   <th>Interface 2.0</th> 
   <th> </th> 
   <th>1.3 Nome do Evento</th> 
   <th>1.3 Interface</th> 
  </tr> 
  <tr> 
   <td><p>(suprimido para 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>preparado</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdates</p> <p>Quando um item de media player é atualizado.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>atualizado</p> <p>Quando o player de mídia tiver atualizado a mídia com êxito.</p> </td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TtmedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdates</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>TtmelineUpdates</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>Excluído em 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>Excluído para 2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>stateChanged</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>SizeEvent</td> 
   <td> </td> 
   <td>tamanho</td> 
   <td>SizeEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adStarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>NotificationStart</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>adCompleted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>timeChanged</td> 
   <td>TimeEvent</td> 
   <td> </td> 
   <td>time</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>progresso</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>searchBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>searchStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>searchEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>searchComplete</td> 
   <td>loadEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>adInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>bufferEvent</td> 
   <td> </td> 
   <td>operationFailed</td> 
   <td>ErrorEvent</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reserveReached</td> 
   <td>ReservationEvent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TimelineHolderEvent</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSeleted</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>rateSeleted</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClicou<br /> quando o usuário clica em um anúncio.</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Quando o perfil de reprodução muda.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>searchPositionAjusted<br /> Quando a posição de busca se ajusta devido a regras internas ou externas.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioAtualizado<br /> quando um item de media player é atualizado. Para determinados fluxos que contêm faixas de áudio que são detectáveis somente no tempo de reprodução, esse evento é disparado quando novas faixas de áudio estão disponíveis.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>legendasAtualizadas <br /> quando um item de player de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdates <br /> Quando um item de media player é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeAtualizado<br /> quando um item de player de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Enviado quando eventos cronometrados são gerados.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface ABRControlParameters<br /> {<br /> const abreviado não assinado ABR_POLICY_CONSERVATIVE = 0 ;<br /> const abreviado não assinado ABR_POLICY_MODERATE = 1 ;<br /> const abreviado não assinado ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute short abrPolicy não assinado;<br /> Atributo unsigned int initialBitRate;<br /> Atributo unsigned int minBitRate;<br /> Atributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const abreviado não assinado ABR_POLICY_CONSERVATIVE = 0 ;<br /> const abreviado não assinado ABR_POLICY_MODERATE = 1 ;<br /> const abreviado não assinado ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute short abrPolicy não assinado;<br /> Atributo unsigned int initialBitRate;<br /> Atributo unsigned int minBitRate;<br /> Atributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface BufferControlParameters<br /> {<br /> duplo de atributo initialBufferTime;<br /> duplo do atributo playBufferTime;<br /> const duplo DEFAULT_INITIAL_BUFFER_TIME;<br /> const duplo DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> duplo de atributo initialBufferTime;<br /> duplo do atributo playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const short COLOR_BLACK não assinado = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const short COLOR_WHITE não assinado = 3 ;<br /> const short COLOR_BRIGHT_WHITE não assinado = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const short COLOR_BRIGHT_RED não assinado = 7 ;<br /> const short COLOR_DARK_GREEN não assinado = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const short COLOR_BRIGHT_GREEN não assinado = 10 ;<br /> const short COLOR_DARK_BLUE não assinado = 11 ;<br /> const short COLOR_BLUE não assinado = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const short COLOR_DARK_YELLOW não assinado = 14 ;<br /> const short COLOR_YELLOW não assinado = 15 ;<br /> const short COLOR_BRIGHT_YELLOW não assinado = 16 ;<br /> const short COLOR_DARK_MAGENTA não assinado = 17 ;<br /> const short COLOR_MAGENTA não assinado = 18 ;<br /> const short COLOR_BRIGHT_MAGENTA não assinado = 19 ;<br /> const short COLOR_DARK_CYAN não assinado = 20 ;<br /> const short COLOR_CYAN não assinado = 21 ;<br /> const short COLOR_BRIGHT_CYAN não assinado = 22 ;<br /> <br /> Atributo readonly fontColor abreviado não assinado;<br /> Atributo readonly short backgroundColor não assinado;<br /> Atributo readonly fill short fillColor não assinado;<br /> atributo readonly edgeColor não assinado;<br /> <br /> // Tamanho<br /> const unsigned short SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const short SIZE_MEDIUM não assinado = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> atributo readonly de tamanho curto não assinado;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const short FONT_EDGE_DROP_SHADOW_RIGHT não assinado = 6 ;<br /> atributo readonly fontEdge abreviado não assinado;<br /> <br /> // Fonte<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const short FONT_CASUAL não assinado = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const short FONT_SMALL_CAPITALS não assinado = 6 ;<br /> atributo readonly de fonte curta não assinada;<br /> atributo readonly font short não assinadoOpacity;<br /> atributo readonly short backgroundOpacity não assinado;<br /> Atributo readonly unsigned short fillOpacity;<br /> Atributo readonly unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> void load(recurso MediaResource, long resourceId,<br /> ouvinte ItemLoaderListener, configuração <br /> MediaPlayerItemConfig) ;<br /> void cancel();<br /> atributo readonly MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Novo para o 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>Novo para o 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API de características de mídia para 2.0 {#media-characteristics-api-element-changes-for}

Essas tabelas comparam os elementos da API de características de mídia para o C++ TVSDK entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* MediaPlayerItem
* Track, AudioTrack, ClosedCaptionsTrack
* Perfil
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {<br /> atributo somente leitura: recurso MediaResource;<br /> Atributo readonly resourceId longo;<br /> Atributo somente leitura: booliano live;<br /> <br /> atributo readonly boolean hasAlternateAudio;<br /> Atributo somente leitura AudioTrackList audioTracks;<br /> atributo readonly AudioTrack seletedAudioTrack;<br /> void selectAudioTrack(faixa AudioTrack); <br /> <br /> atributo readonly boolean hasClosedCaptions;<br /> atributo readonly ClosedCaptionsTrackList closedCaptionsTracks;<br /> atributo readonly ClosedCaptionsTrack seletedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> faixa ClosedCaptionsTrack); <br /> <br /> atributo readonly boolean hasTimedMetadata;<br /> o atributo só de leitura TimedMetadataList timedMetadata;<br /> Atributo somente leitura: booliano dinâmico;<br /> <br /> o atributo readonly boolean isProtected;<br /> atributo readonly DRMMetadataInfoList drmMetadataInfos;<br /> Atributo readonly perfis ProfileList;<br /> perfil do atributo readonly seletedProfile;<br /> <br /> atributo readonly trickPlaySupported booleano;<br /> atributo readonly FloatArray availablePlaybackRates;<br /> atributo readonly float selatPlaybackRate;<br /> <br /> <br /> Atributo readonly MediaPlayer mediaPlayer;<br /> Atributo readonly atributo MediaPlayerItemConfig config;<br /> };</p> </td> 
   <td><p>interface MediaPlayerItem {<br /> atributo somente leitura: recurso MediaResource;<br /> Atributo readonly resourceId longo;<br /> Atributo somente leitura: booliano live;<br /> <br /> atributo readonly boolean hasAlternateAudio;<br /> Atributo somente leitura AudioTrackList audioTracks;<br /> Atribuir AudioTrack seletedAudioTrack;<br /> <br /> <br /> atributo readonly boolean hasClosedCaptions;<br /> atributo readonly ClosedCaptionsTrackList ccTracks;<br /> Atributo ClosedCaptionsTrack seletedCCTrack;<br /> <br /> <br /> <br /> atributo readonly boolean hasTimedMetadata;<br /> o atributo só de leitura TimedMetadataList timedMetadata;<br /> Atributo somente leitura: booliano dinâmico;<br /> <br /> o atributo readonly boolean isProtected;<br /> atributo readonly DRMMetadataInfoList drmMetadataInfos;<br /> Atributo readonly perfis ProfileList;<br /> <br /> <br /> atributo readonly trickPlaySupported booleano;<br /> atributo readonly Int32Array availablePlaybackRates;<br /> <br /> atributo readonly StringList adTags;<br /> <br /> Atributo readonly MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> atributo somente leitura Nome DomString;<br /> Atributo somente leitura Linguagem DomString;<br /> atributo readonly default booleano;<br /> atributo readonly autoSelect booleano;<br /> }; </p> </td> 
   <td>Novo para o 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Rastrear<br /> {<br /> atributo somente leitura Nome DomString; //FromTrack<br /> atributo somente leitura Linguagem DomString;//FromTrack<br /> atributo somente leitura booleano padrão; // Do atributo somente leitura Track<br /> autoSelect;//FromTrack<br /> atributo somente leitura <br /> unsigned int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> atributo somente leitura Nome DomString;<br /> Atributo somente leitura Linguagem DomString; <br /> atributo readonly default booleano;<br /> atributo readonly autoSelect booleano;<br /> Atributo somente leitura booleano forçado;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> atributo readonly comprimento longo não assinado;<br /> getter AudioTrack (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Rastrear<br /> {<br /> atributo somente leitura Nome DomString; //FromTrack<br /> atributo somente leitura Linguagem DomString;//FromTrack<br /> atributo somente leitura booleano padrão; // Atributo somente leitura FromTrack<br /> boolean autoSelect;//FromTrack<br /> <br /> <br /> const short SERVICE_608_CAPTIONS não assinado = 0;<br /> const short SERVICE_708_CAPTIONS = 1;<br /> const short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> readonly attribute unsigned short serviceType;<br /> Atributo somente leitura booleano forçado;<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> atributo somente leitura Nome DomString;<br /> Atributo somente leitura Linguagem DomString;<br /> atributo readonly default booleano;<br /> <br /> <br /> atributo readonly boolean ative;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> atributo readonly unsigned long length;<br /> getter ClosedCaptionsTrack(índice longo não assinado);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Perfil {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Perfil: Nenhuma alteração para 2.0</td> 
   <td><p>perfil<br /> de interface {<br /> atributo readonly unsigned int width;<br /> atributo readonly unsigned int height;<br /> atributo readonly int int bitRate não assinado;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: Nenhuma alteração para 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> atributo readonly unsigned long length;<br /> perfil getter (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>: Nenhuma alteração para 2.0</td> 
   <td><p>interface DRMMetadataInfo<br /> { <br /> atributo somente leitura metadados DRMMetadata;<br /> atributo readonly long prefetchTimestamp;<br /> atributo readonly TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Nenhuma alteração para 2.0</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> atributo readonly unsigned long length;<br /> getter DRMMetadataInfo (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Mapeamento de erros C++ para exceções em diferentes idiomas {#mapping-c-errors-to-exceptions-in-different-languages}

É possível mapear códigos de erro C++ para exceções em idiomas diferentes.

O PSDK C++ tem uma política de &quot;sem lançamento&quot; para suas APIs. A maioria dos métodos de API retorna um valor PSDKErrorCode para indicar se o método foi executado com êxito. Erros assíncronos são notificados por meio dos eventos de erro.

O PSDK do ActionScript e JAVA tem uma política diferente. A maioria dos erros exibirá ArgumentError ou IllegalStateException para indicar que a parte síncrona do método não pôde ser executada. Essas exceções não são capturadas, e o código do aplicativo é responsável por lidar com as exceções. Geralmente, eles apresentam informações úteis sobre por que a chamada de método falhou. Por exemplo, se o comando prepareToPlay for chamado em um estado inválido, a seguinte exceção será lançada:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

O ActionScript/JAVA também lança exceções de construtores para indicar que algum objeto interno foi criado incorretamente. Essas exceções são tratadas internamente e não são propagadas para o aplicativo. As exceções serão incluídas em uma notificação de aviso enviada ao aplicativo

Por exemplo, se nenhum arquivo de mídia válido foi encontrado para a resposta de anúncio recebida, nenhum objeto de ativo de anúncio ou anúncio válido pode ser criado. Como resultado, nenhum anúncio é colocado na linha do tempo e uma notificação NotificationEvent.OperationFailed é enviada.

Os códigos de erro ou aviso recebidos de forma assíncrona do Adobe Video Engine (AVE) são enviados para o aplicativo como eventos normais. O evento de notificação contém todos os códigos de erro recebidos e quaisquer metadados adicionais, como URL, identificador de recurso, identificador e assim por diante. Se o erro for grave e a reprodução da mídia atual não puder continuar, o MediaPlayer será transição para o status ERROR e o retorno de chamada onStatusChanged ou MediaPlayerStatusChanged.STATUS_CHANGED será despachado. Se a reprodução puder continuar, um evento de notificação normal será despachado.

<table> 
 <tbody> 
  <tr> 
   <th>Erro C++ (código de erro PSDKError)</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Exceção com código = 1, descrição = "INVALID_ARGUMENT" e additionalInfo= &lt;como aprovado pelo método que acionou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Exceção com código = 2, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme aprovado pelo método que lançou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Exceção com código = 3, descrição = "ILLEGAL_STATE" e additionalInfo= &lt;conforme aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 4, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme aprovado pelo método que lançou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 5, descrição = "CREATION_FAILED" e additionalInfo= &lt;conforme aprovado pelo método que lançou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 5, descrição = "CREATION_FAILED" e additionalInfo= &lt;conforme aprovado pelo método que lançou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 7, descrição = "DATA_NOT_AVAILABLE" e additionalInfo= &lt;como aprovado pelo método que acionou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 8, descrição = "SEEK_ERROR" e additionalInfo= &lt;como aprovado pelo método que acionou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 9, descrição = "UNSUPPORTED_FEATURE" e additionalInfo= &lt;conforme aprovado pelo método que lançou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 10, descrição = "RANGE_ERROR" e additionalInfo= &lt;como aprovado pelo método que lançou esta exceção</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 11, descrição = "CODEC_NOT_SUPPORTED" e additionalInfo= &lt;conforme aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 12, descrição = "MEDIA_ERROR" e additionalInfo= &lt;como aprovado pelo método que lançou esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 13, descrição = "NETWORK_ERROR" e additionalInfo= &lt;como aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error ou MediaPlayerNotification.Warning</td> 
   <td>MediaError ou NotificationEvent</td> 
   <td>Exceção com código = 14, descrição = "GENERIC_ERROR" e additionalInfo= &lt;como aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 15, descrição = "INVALID_SEEK_TIME" e additionalInfo= &lt;conforme aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 16, descrição = "AUDIO_TRACK_ERROR" e additionalInfo= &lt;conforme aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 17, descrição = "GENERIC_ERROR" e additionalInfo= &lt;como aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 18, descrição = "GENERIC_ERROR" e additionalInfo= &lt;como aprovado pelo método que lançou esta exceção</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 19, descrição = "GENERIC_ERROR" e additionalInfo= &lt;como aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 200, descrição = "PLAYBACK_OPERATION_FAILED" e additionalInfo= &lt;como aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Exceção com código = 201, descrição = "NATIVE_WARNING" e additionalInfo= &lt;conforme aprovado pelo método que lançou esta exceção</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Exceção com código = 202, descrição = "AD_RESOLVER_FAILED" e additionalInfo= &lt;conforme aprovado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Alterações de elementos de API de utilitário e auxiliar para 2.0 {#utility-and-helper-api-element-changes-for}

Essas tabelas comparam os elementos da API Utilitário e Auxiliar para o JavaScript TVSDK entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* Versão
* TimeRange
* QOSProvider
* DeviceInformation
* LoadInfo
* Visualização
* ReproduçãoInformações

### Versão {#version}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>versão<br /> da interface {<br /> atributo somente leitura versão DomString;<br /> descrição do atributo somente leitura DomString;<br /> Atribuir somente leitura longa major;<br /> atributo readonly minor;<br /> Atribuir somente leitura a revisão longa;<br /> Atributo readonly long apiVersion;<br /> };</p> </td> 
   <td><p>versão<br /> da interface {<br /> atributo somente leitura versão DomString;<br /> descrição do atributo somente leitura DomString;<br /> atributo readonly DomString major;<br /> atributo readonly DomString minor;<br /> atributo readonly revisão DomString;<br /> atributo readonly DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface TimeRange<br /> {<br /> atributo readonly long begin; não assinado;<br /> atributo readonly long end não assinado;<br /> atributo readonly de longa duração não assinada;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> atributo readonly DeviceInformation deviceInformation;<br /> atributo readonly PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DeviceInformation {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface DeviceInformation<br /> {<br /> atributo somente leitura DomString os;<br /> <br /> <br /> <br /> atributo readonly DomString id;<br /> atributo readonly int DPI;<br /> atributo readonly int heightPixels;<br /> atributo readonly int widthPixels;<br /> atributo readonly request boolean searchToKeyFrame;<br /> };</p> </td> 
   <td><p>interface DeviceInformation<br /> {<br /> atributo somente leitura DomString os;<br /> atributo readonly int sdk;<br /> atributo readonly modelo DomString;<br /> atributo readonly do fabricante DomString;<br /> atributo readonly DomString id;<br /> atributo readonly int DPI;<br /> atributo readonly int heightPixels;<br /> atributo readonly int widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface LoadInfo<br /> {<br /> atributo somente leitura url DomString;<br /> atributo readonly int tamanho int;<br /> readonly attribute duplo downloadDuration;<br /> atributo readonly int periodIndex;<br /> Atributo readonly mediaDuration do duplo;<br /> atributo readonly short TRACK_TYPE_FRAGMENT;<br /> atributo readonly short TRACK_TYPE_TRACK;<br /> atributo readonly short TRACK_TYPE_MANIFEST;<br /> tipo abreviado do atributo readonly;<br /> atributo readonly DomString trackName;<br /> atributo readonly DomString trackType;<br /> Atributo readonly em trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Visualização {#view}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>visualização<br /> da interface {<br /> atributo readonly unsigned short x;<br /> Atributo readonly unsigned short y;<br /> Atributo somente leitura de largura curta não assinada;<br /> Atributo readonly de altura curta não assinada;<br /> <br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### ReproduçãoInformações {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute duplo timeToFirstByte;<br /> Atributo readonly duplo timeToLoad;<br /> Atributo readonly timeToStart; duplo timeToStart;<br /> Atributo readonly timeToFail do duplo;<br /> atributo readonly int totalSecondsPlayed;<br /> atributo readonly int totalSecondsSpent;<br /> atributo readonly duplo frameRate;<br /> atributo readonly int droppedFrameCount;<br /> Atributo readonly intBandwidth;<br /> atributo readonly int na taxa de bits;<br /> defaultTime do duplo do atributo readonly;<br /> atributo readonly int bufferLength;<br /> atributo readonly em emptyBufferCount;<br /> Atributo readonly attribute duplo bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> readonly attribute duplo timeToFirstByte;<br /> Atributo readonly duplo timeToLoad;<br /> Atributo readonly timeToStart; duplo timeToStart;<br /> Atributo readonly timeToFail do duplo;<br /> atributo readonly int totalSecondsPlayed;<br /> atributo readonly int totalSecondsSpent;<br /> atributo readonly duplo frameRate;<br /> atributo readonly int droppedFrameCount;<br /> <br /> atributo readonly int na taxa de bits;<br /> defaultTime do duplo do atributo readonly;<br /> atributo readonly int bufferLength;<br /> atributo readonly em emptyBufferCount;<br /> Atributo readonly attribute duplo bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos úteis {#helpful-resources}

* Consulte a documentação completa da ajuda na página Aprendizagem e suporte [da](https://helpx.adobe.com/support/primetime.html) Adobe Primetime.
