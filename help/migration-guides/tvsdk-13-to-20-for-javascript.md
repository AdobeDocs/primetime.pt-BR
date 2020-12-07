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

## Implementar funções de retorno de chamada em JavaScript {#implement-callback-functions-in-javascript}

Os comentários na documentação do método sugerem a assinatura para retornos de chamada que você precisa implementar.

Para JavaScript, a sintaxe da API se baseia na ID da Web. Para uma interface TVSDK, os nomes do método são chamados *methodName*(). Para que os métodos sejam implementados pelo aplicativo, um atributo de leitura/gravação chamado *methodName* CallbackFunc é adicionado à interface e seu aplicativo deve defini-lo para apontar para uma função que implementa o método. Por exemplo:

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
   <td><p> <strong>TimedMetadata</strong>: interface TimedMetadata {<br /> const short METADATA_TYPE_TAG = 0 ;  <br /> const short METADATA_TYPE_ID3 não assinado = 1 ;  <br /> tipo abreviado não assinado do atributo readonly;  <br /> Atributo readonly long time;atributo <br /> readonly DomString id;atributo <br /> readonly DomString name;atributo <br /> readonly DomString content;  <br /> Atributo somente leitura Metadados do objeto;<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const short METADATA_TYPE_TAG = 0 ;<br /> const unsigned short METADATA_TYPE_ID3 = 1 ;<br /> atributo readonly somente de leitura metadataType;<br /> atributo readonly long time;<br /> readonly attribute long id;<br /> atributo readonly DomString;<br /> <br /> atributo somente leitura Metadados do objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> atributo somente leitura de comprimento longo não assinado;<br /> getter TimedMetadata (índice longo não assinado);<br /> };</p> </td> 
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
   <td><p>Interface AdSignalingMode { <br /> const. short MODE_DEFAULT não assinado, <br /> const. short MODE_MANIFEST_CUES não assinado, <br /> const. short MODE_SERVER_MAP não assinado, <br /> const. short MODE_CUSTOM_RANGES <br /> };</p> </td> 
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
   <td><p>Atributo AdSignalingMode { <br /> da interface AdvertisingMetadata {&lt;a0/&gt;; Atributo <br /> AdBreakWatchedPolicy adBreakAsWatched; atributo <br /> boolean livePreroll; atributo <br /> delayAdLoading booleano ; <br /> };</p> </td> 
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
   <td><p>Interface CustomRangeMetadata { <br /> const short TYPE_MARK_RANGE não assinado; <br /> const short não assinado TYPE_DELETE_RANGE; <br /> const short não assinado TYPE_REPLACE_RANGE; Atributo <br /> tipo abreviado não assinado; atributo <br /> booliano adjustSeekPosition; atributo <br /> TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> atributo long begin unsigned; <br /> atributo readonly unsigned long end; Atributo <br /> de longa duração não assinado; atributo <br /> long replaceDuration não assinado; <br /> };</p> </td> 
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
   <td><p>Posicionamento da interface { <br /> const short TYPE_MID_ROLL não assinado; <br /> const short não assinado TYPE_PRE_ROLL; <br /> const short não assinado TYPE_POST_ROLL; <br /> const short não assinado TYPE_SERVER_MAP; <br /> atributo somente leitura não assinado TYPE_CUSTOM_RANGE;<br /> tipo curto não assinado; <br /> atributo somente leitura por muito tempo; <br /> atributo somente leitura de longa duração; <br /> const short MODE_DEFAULT não assinado; <br /> const short MODE_INSERT não assinado; <br /> const short MODE_REPLACE não assinado; <br /> const short MODE_DELETE não assinado; <br /> const short MODE_MARK não assinado; <br /> const short MODE_FREE_REPLACE não assinado; <br /> atributo readonly atributo unsigned short mode; <br /> atributo somente leitura Intervalo de tempo; <br /> };</p> </td> 
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
   <td><p>interface Opportunity { <br /> atributo somente leitura ID DomString; <br /> posicionamento do atributo somente leitura; <br /> configurações de Objeto de atributo somente leitura; <br /> atributo readonly object customParameters; <br /> }; </p> </td> 
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
   <td><p>reserva de interface { <br /> atributo somente leitura Intervalo de tempo; <br /> atributo somente leitura com retenção longa; <br /> }; </p> </td> 
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
   <td><p><strong>Linha do tempo</strong>: linha do tempo da interface  <br /> { atributo somente leitura TimelineMarkerList timelineMarkers;  <br /> atributo readonly TimelineItemList timelineItems;  <br /> duplo convertToLocalTime( hora do duplo);  <br /> duplo convertToVirtualTime (hora do duplo);  <br /> };</p> </td> 
   <td><p>linha do tempo da interface {<br /> atributo somente leitura TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>Item</strong> da linha do tempo: interface TimelineItem:<br /> TimelineMarker {<br /> readonly attribute long id;  <br /> atributo readonly TimeRange virtualRange;  <br /> atributo readonly TimeRange localRange;  <br /> atributo readonly boolean assistido;  <br /> atributo readonly booliano temporário;  <br /> }; </p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>MarcadorLinha</strong> do tempo: (Sem alteração para 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> tempo do duplo do atributo somente leitura;<br /> duração do duplo do atributo somente leitura;<br /> };</p> </td> 
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
   <td><p>interface AdBreak {<br /> <br /> <br /> <br /> duração do duplo do atributo somente leitura;<br /> atributo somente leitura AdList ads;<br /> <br /> <br /> atributo somente leitura AdInsertionType insertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> hora do duplo do atributo somente leitura;<br /> duplo do atributo somente leitura replaceDuration;<br /> <br /> duração do duplo do atributo somente leitura;<br /> atributo somente leitura AdList adList;<br /> <br /> atributo somente leitura DomString data;<br /> <br /> }; </p> </td> 
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
   <td><p> <strong>Anúncio</strong>: interface Ad {atributo <br /> readonly AdAsset PrimaryAsset;atributo <br /> readonly AdAssetList companionAssets;duração do duplo do atributo <br /> <br /> readonly;atributo DomString id;<br /> const short ADTYPE_LINEAR não assinado = 0;<br /> const short não assinado ADTYPE_NONLINEAR = 1;atributo <br /> readonly short ad Type não assinado;<br /> <br />  <br /> Tipo somente o atributo AdInsertionType adInsertionType;  <br /> <br /> atributo readonly booleano clicável;  <br /> o atributo readonly boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {<br /> atributo somente leitura AdAsset PrimaryAsset;<br /> atributo somente leitura AdAssetList companionAssets;<br /> <br /> duração do duplo do atributo somente leitura;<br /> atributo somente leitura DomString id;<br /> const short não assinado ADTYPE_LINEAR = 0 ;<br /> const short ADTYPE não assinado_NONLINEAR = 1 ;<br /> <br /> atributo somente leitura tipo curto não assinado;<br /> atributo somente leitura AdInsertionType insertionType; <br /> atributo somente leitura Rastreador de objetos;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdAsset {<br /> atributo somente leitura ID DomString;<br /> duração do duplo do atributo somente leitura;<br /> atributo somente leitura Recurso MediaResource;<br /> atributo somente leitura AdClick adClick;<br /> atributo somente leitura Metadados do objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdClick {<br /> atributo somente leitura ID DomString;<br /> atributo somente leitura Título DomString;<br /> atributo somente leitura url DomString;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdList {<br /> atributo somente leitura de comprimento longo não assinado;<br /> getter Ad (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdAssetList {<br /> atributo readonly de comprimento longo não assinado;<br /> getter AdAsset (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interface AdBannerAsset: AdAsset<br /> {atributo somente <br /> leitura na largura;atributo somente <br /> leitura na altura;atributo somente <br /> leitura DomString staticUrl;atributo somente <br /> leitura Altura DomString;largura DomString do atributo somente <br /> leitura;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : Item da linha do tempo { atributo somente  <br /> leitura AdBreak adBreak;  <br /> itens AdTimelineItemList do atributo readonly;  <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : Item da linha do tempo { atributo somente  <br /> leitura AdBreak adBreak;  <br /> atributo somente leitura Anúncio;  <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { atributo  <br /> readonly unsigned long length;  <br /> getter AdBreakTimelineItem (índice ng não assinado);  <br /> };</p> </td> 
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
   <td><p> interface AdPolicyConstants {<br /> atributo readonly short AD_BREAK_POLICY_SKIP;<br /> atributo readonly short AD_BREAK_POLICY_PLAY;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE;<br /> atributo readonly short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly short AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly short AD_BREAK_AS_WATCHED_NEVER;&lt;a3 &gt; };<br /> </p> </td> 
   <td><p> ...<br /> atributo readonly abreviado AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo readonly curto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo readonly abreviado AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> atributo readonly short AD_POLICY_PLAY;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; atributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo readonly short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br /> atributo readonly short AD_POLICY_PLAY;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo readonly short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo readonly short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK; <br /> atributo readonly abreviado AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> atributo readonly short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> atributo readonly short AD_POLICY_MODE_SEEK;<br /> atributo readonly short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> atributo somente leitura AdTimelineItem adTimelineItem;<br /> duplo de atributo somente leitura currentTime;<br /> atributo readonly duplo requestToTime;&lt;a5/ taxa de duplo do atributo somente leitura;<br /> modo abreviado do atributo somente leitura; //AdPolicyMode<br /> };<br /></p> </td> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakPlacementList <br /> adBreakPlacements;<br /> atributo somente leitura Ad;<br /> duplo de atributo somente leitura currentTime;<br /> atributo somente leitura Taxa de duplo do atributo requestToTime;<br /> readonly modo abreviado do atributo readonly; //AdPolicyMode<br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForAdBreakCallbackFunc;<br />* a6/&gt; * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo O objeto selectAdBreaksToPlayCallbackFunc;<br /> /*<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo O objeto selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBreak akCallbackFunc;<br /> };<br /></p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForAdBreakFuncCallback;<br />* a6/&gt; * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectAdBreaksToPlayCallback;<br /> /*<br /> * dPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBreak akCallback;<br /> };<br /></p> </td> 
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
   <td><p>interface Linha do tempoOperação { <br /> posicionamento do atributo somente leitura ; <br /> };</p> </td> 
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
   <td><p>interface AdBreakPlacement: Linha do tempoOperação {<br /> atributo somente leitura AdBreak adBreak;<br /> colocação de disposição de atributo somente leitura; // From TimelineOperation<br /> tempo do duplo do atributo somente leitura;<br /> duração do duplo do atributo somente leitura;<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> atributo somente leitura AdBreak adBreak;<br /> colocação do atributo somente leitura;<br /> hora do duplo do atributo somente leitura;<br /> duração do duplo do atributo somente leitura;<br /> };</p> </td> 
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
   <td><p>interface AuditudeSettings: AdvertisingMetadata { <br /> atributo DomString zoneId; atributo <br /> DomString mediaId; Atributo <br /> DomString defaultMediaId ; Atribua <br /> domínio DomString ; Atribua <br /> Object targettingInfo ; Atribua <br /> Object customParameters ; atributo <br /> Boolean creativePackaingEnabled ;<br /> atributo Boolean showStaticBanners ;<br /> };</p> </td> 
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
   <td><p>atributo MediaPlayerItemConfig {<br /> atributo ContentFactory adFactory;<br /> atributo StringList subscribeTags;<br /> atributo StringList adTags;<br /> <br /> atributo AdSignalingMode adSignalingSignaling;<br /> attributeCustom O atributo customRangeMetadata;<br /> NetworkConfiguration;<br /> do atributo AdvertisingMetadata advertiadataMetadata;<br /> Atributo Uso boolianoHardwareDecoder;<br /> };<br /><br /></p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /> atributo <br /> <br /> StringList adTags;<br /> atributo StringList subscriptionTags;<br /> atributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem item);<br /> */<br /> atributo Object retrieveAdPolicySeletorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * item MediaPlayerItem);<br /> */<br /> atributo Object retrieveAdPolicySeletorFunc;<br /> };</p> </td> 
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
   <td><p>interface NetworkConfiguration<br /> atributo {<br /> boolean forceNativeNetworking;<br /> atributo boolean useRedirectUrl;<br /> atributo Object cookieHeader;<br /> atributo boolean readSetCookieHeader;<br /> atributo int masterUpdateInterval; atributo <br /> booliano useCookieHeaderForAllRequests;<br /> atributo int readLimit;<br /> };</p> </td> 
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
   <td>O aplicativo precisa chamar o AdobePSDK.initiDRMWorkflow para iniciar o fluxo de trabalho do DRM. Sem esta chamada, os vídeos DRM não serão reproduzidos.<p>interface AdobePSDK<br /> {<br /> void startDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> booleanMode On);<br /> };</p> </td> 
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
   <td><p>interface DRMMetadata<br /> {<br /> atributo somente leitura DomString serverUrl;<br /> atributo somente leitura DomString licenseId;<br /> atributo somente leitura DRMPolicyArray políticas; <br /> };</p> </td> 
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
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo somente leitura em playbackPeriodInSeconds;<br /> atributo readonly playbackStartDate;<br /> atributo readonly long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo readonly int periodInSeconds;<br /> atributo readonly int startDate;<br /> atributo readonly int endDate;<br /> };</p> </td> 
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
   <td><p>interface DRMLicense {<br /> atributo somente leitura Bytes Uint8Array;<br /> atributo somente leitura Date licenseStartDate;<br /> atributo somente leitura Date licenseEndDate;<br /> atributo somente leitura Data offlineStorageStartDate;<br /> atributo somente leitura Data offlineStorageEndDate; <br /> atributo somente leitura DomString serverUrl;<br /> atributo somente leitura DomString licenseID;<br /> atributo somente leitura DomString policyID;<br /> atributo somente leitura DRMPlaybackTimeWindow playbackTimeWindow;<br /> atributo somente leitura Object customProperties;<br /> }; </p> </td> 
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
   <td><p>interface DRMLicenseDomain {<br /> atributo somente leitura DomString authenticationDomain;<br /> atributo somente leitura DRMAuthenticationMethod authenticationMethod; <br /> atributo somente leitura DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br /> atributo somente leitura DomString authDomain;<br /> atributo somente leitura DRMAuthenticationMethod authMethod; <br /> atributo somente leitura DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPolicy<br /> {<br /> atributo somente leitura Atributo DomString authenticationDomain;<br /> atributo somente leitura DRMAuthenticationMethod authenticationMethod;<br /> <br /> atributo somente leitura DomString displayName;<br /> atributo somente leitura DRMLicenselicenseDomain;<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {<br /> atributo somente leitura DomString authDomain;<br /> atributo somente leitura DRMAuthenticationMethod authMethod;<br /> atributo somente leitura DomString dispName;<br /> atributo somente leitura DRMLicenseLiclicenseDomain;<br /> };</p> </td> 
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
   <td><p>interface DRMManager: EventTarget {<br /> void acquisitionLicense(metadados DRMMetadata, <br /> configuração DRMAcquireLicenseSettings, <br /> DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(metadados DRMMetadata, <br /> DRMAquireLicense listener do enseListener);<br /> void authenticate(metadados DRMMetadata, <br /> URL DomString,<br /> DomString &amp;authenticationDomain, <br /> Usuário DomString, <br /> Senha DomString, <br /> Listener DRMAuthenticateListener);&lt;a 11/&gt; <br /> DRMMetadata createMetadataFromBytes(<br /> matriz Uint8Array, ouvinte DRMErrorListener);<br /> void initialize(ouvinte DRMOperationCompleteListener);<br /> atributo long maxOperation Time;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener listener listener);<br /> voidLicense Domain(<br /> DRMLicenseDomain licenseDomain, <br /> ouvinte DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener);<br /> void returnLicense(Dom String serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> boolean commitImediatamente,<br /> DRMReturnLicenseListener listener);<br /> void setAuthenticationToken(&lt;a 32/&gt; Metadados DRMMetadata, <br /> Autenticação DomStringDomain, <br /> token Uint8Array, <br /> listener DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, &lt;a3 7/&gt; Ouvinte DRMOperationCompleteListener);<br /> };<br /><br /><br /></p> </td> 
   <td><p>interface DRMManager: EventTarget {<br /> void acquisitionLicense(metadados DRMMetadata, <br /> configuração DRMAcquireLicenseSettings, <br /> EventContextContext);<br /> void acquisitionPreviewLicense(metadados DRMMetadata, <br /> EventContext);&lt;a5&gt; void authenticate(metadados DRMMetadata, <br /> URL DomString,<br /> DomString &amp;authenticationDomain, <br /> usuário DomString, <br /> Senha DomString, <br /> EventContext eventContext);<br /> <br /> DRMM etadata createMetadataFromBytes(<br /> matriz Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain (<br /> DRMLicenseDomain licenseDomain, <br /> booleano forceRefresh, <br /> EventContext);<br /> void LeaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, &lt;a2 commitImediatamente booleano,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> Metadados DRMMetadata, <br /> DomString authenticationDomain, <br /> Token Uint8Array, &lt;a EventContext (EventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };<br /><br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMErrorListener: <br /> psdkutils públicos::PSDKInterfaceWithUserData {<br /> public:<br /> vazio virtual onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protegido:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando um erro ocorre durante um dos métodos assíncronos do DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMOperationCompleteListener: <br /> DRMErrorListener público {<br /> public:<br /> void virtual onDRMOperationComplete() = 0;<br /> <br /> protected:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
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
   <td><p>classe DRMAuthenticateListener: <br /> DRMErrorListener público {<br /> public:<br /> void virtual onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protegido:<br /> ~DRMA authenticateListener() {}<br /> }</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Quando a chamada de método DRMManager::authenticate for bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAquireLicenseListener: <br /> DRMErrorListener público {<br /> public:<br /> vazio virtual onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionPreviewLicense for bem-sucedida.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionLicense for bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMReturnLicenseListener: <br /> DRMErrorListener público {<br /> public:<br /> vazio virtual onLicenseReturnComplete(uint32_t numReturn ) = 0;<br /> <br /> protegido:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / interface / descrição 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Quando a chamada do método DRMManager::returnLicense for bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Alterações genéricas no elemento da API de reprodução para 2.0 {#generic-playback-api-element-changes-for}

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
   <td><p>interface MediaResource {<br /> atributo DomString url; Atributo <br /> tipo curto não assinado;<br /> atributo Metadados do objeto;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN; a 8/&gt; };<br /></p> </td> 
   <td><p>interface MediaResource {<br /> atributo DomString url;<br /> atributo DomString type;<br /> atributo Metadados do objeto;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay( posição do duplo);<br /> void play();<br /> void pause();<br /> void search( posição do duplo);<br /> void searchToLocal( posição do duplo);<br /> void reset();<br /> void release(); a8/&gt; void replaceCurrentItem(item MediaPlayerItem);<br /> void replaceCurrentResource(recurso MediaResource, <br /> configuração MediaPlayerItemConfig); <br /> void drop();<br /> void restore();<br /> void notificationClick();<br /> <br /> atributo só de leitura TimeRange playbackRange;<br /> atributo somente de leitura TimeRange SekableRange;<br /> <br /> duplo de atributo readonly currentTime;<br /> atributo readonly duplo localTime;<br /> atributo readonly TimeRange bufferedRange;<br /> atributo readonly DRMManager drmManager;<br /> atributo readonly MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> &lt;a7&gt; <br /> const short não assinado PLAYER_STATUS_INITIALIZED;<br /> const short não assinado PLAYER_STATUS_PREPARING;<br /> const short não assinado PLAYER_STATUS_PREPARED;<br /> const short não assinado PLAYER_STATUS_PLAYING;&lt;a12&gt; const short não assinado PLAYER_STATUS_PAUSED;<br /> const short não assinado PLAYER_STATUS_SEEKING;<br /> const short não assinado PLAYER_STATUS_COMPLETE;<br /> const short não assinado PLAYER_STATUS_ERROR;<br /> const assinado como PLAYER_STATUS_RELEASED;<br /> <br /> <br /><br /> o atributo readonly Atributo status abreviado não assinado;<br /> <br /> atributo de volume curto não assinado;<br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> const de VISIBLE curto não assinado; //For CC Visibilidade<br /> const. curta não assinada INVISÍVEL; //For CC Visibility<br /> atributo ccVisibility não assinado;<br /> atributo TextFormat ccStyle;<br /> atributo readonly PlaybackMetrics playbackMetrics;<br /> Taxa de duplo do atributo <br /> visualização MediaPlayerView;&lt;a13 linha do tempo da Linha do tempo do atributo somente leitura;<br /> duplo do atributo currentTimeUpdateInterval; <br /> // configurar esta opção Não será suportado para 2.0<br /> };<br /><br /></p> </td> 
   <td><p>interface MediaPlayer: EventTarget<br /> {<br /> void prepareToPlay( int position);<br /> void play();<br /> void pause();<br /> void search( int position);<br /> void searchToLocalTime( int position);<br /> void reset();<br /> void release();8/&gt; void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo só de leitura TimeRange playbackRange;<br /> atributo só de leitura TimeRange; <br /> duplo de atributo somente leitura currentTime;<br /> atributo somente leitura duplo localTime;<br /> atributo somente leitura TimeRange bufferedRange;<br /> <br /> atributo somente leitura DRMManager drmManager;<br /> atributo somente leitura MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const. curta PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned PLAYER _STATE_INITIALIZED;<br /> const short não assinado PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const assinado curta PLAYER_STATE_SEEKING;<br /> const short não assinado PLAYER_STATE_COMPLETE;<br /> const short não assinado PLAYER_STATE_ERROR;<br /> const short não assinado PLAYER_STATE_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED;<br /> atributo somente leitura de estado abreviado não assinado;<br /> <br /> atributo de volume curto não assinado;<br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> readonly unsigned short VISIBLE; //For CC Visibilidade<br /> curta não assinada somente para leitura INVISÍVEL; //For CC Visibility<br /> atributo ccVisibility não assinado;<br /> atributo TextFormat ccStyle;<br /> atributo readonly PlaybackMetrics playbackMetrics;<br /> atributo MediaPlayerConfig mediaPlayerConfig;<br /> taxa de duplo do atributo;<br /> atributo MediaPlayerView linha do tempo da linha do tempo do atributo somente leitura;<br /><br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const. curta não assinada PLAYER_STATUS_IDLE;<br /> const. curta não assinada PLAYER_STATUS_INITIALIZING;<br /> const. curta PLAYER_STATUS_INITIALIZED não assinado;<br /> const ER_STATUS_PREPARING;<br /> const short não assinado PLAYER_STATUS_PREPARED;<br /> const short não assinado PLAYER_STATUS_PLAYING;<br /> const short não assinado PLAYER_STATUS_PAUSED;<br /> const short não assinado PLAYER_STATUS_SEEKING;&lt;a10&gt; const short não assinado PLAYER_STATUS_COMPLETE;<br /> const short não assinado PLAYER_STATUS_ERROR;<br /> const short não assinado PLAYER_STATUS_RELEASED;<br /> const short não assinado PLAYER_STATUS_SUSPENDED;<br /> };<br /></p> </td> 
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
   <td>adStart</td> 
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
   <td>progresso</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>buffer</td> 
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
   <td>TimeEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>NotificationEvent</td> 
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
   <td>adClicked<br /> Quando o usuário clica em um anúncio.</td> 
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
   <td>searchPositionReguled<br /> Quando a posição de busca se ajusta devido a regras internas ou externas.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdates<br /> Quando um item de media player é atualizado. Para determinados fluxos que contêm faixas de áudio que são detectáveis somente no tempo de reprodução, esse evento é disparado quando novas faixas de áudio estão disponíveis.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novo no 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>captionsAtualizado <br /> Quando um item de player de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
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
   <td>playbackRangeUpdates<br /> Quando um item de media player é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
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
   <td><p>interface ABRControlParameters<br /> {<br /> const short não assinado ABR_POLICY_CONSERVATIVE = 0 ;<br /> const short não assinado ABR_POLICY_MODERATE = 1 ;<br /> const short não assinado ABR_POLICY_AGGRESIVE = 2 ;<br /> atributo abrPolicy não assinado;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const short DEFAULT_ABR_MIN_MIN BITRATE;<br /> const short DEFAULT_ABR_MAX_BITRATE não assinado;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };<br /></p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const short não assinado ABR_POLICY_CONSERVATIVE = 0 ;<br /> const short não assinado ABR_POLICY_MODERATE = 1 ;<br /> const short não assinado ABR_POLICY_AGGRESIVE = 2 ;<br /> atributo abrPolicy não assinado Atributo;<br /> não assinado int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };<br /></p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br /> duplo de atributo initialBufferTime;<br /> duplo de atributo playBufferTime;<br /> const duplo DEFAULT_INITIAL_BUFFER_TIME;<br /> const duplo DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> duplo de atributo initialBufferTime;<br /> duplo de atributo playBufferTime;<br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const curta não assinada COLOR_BRIGHT_WHITE = 4 ;<br /> const short não assinado COLOR_DARK_RED = 5 ;<br /> const short COLOR_RED não assinado = 6 ;<br /> const short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ; <br /> const short COLOR_GREEN não assinado = 9 ;<br /> const short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ; <br /> const short COLOR_BRIGHT_BLUE sem sinal = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const short COLOR_YELLOW sem sinal = 15 ;<br /> const unsigned short COLOR_BRIGHT_AMARELO = 16 ;<br /> const short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const curta não assinada COLOR_CYAN = 21 ;<br /> const curta não assinada COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> atributo somente leitura não assinado short fontColor;<br /> atributo somente leitura não assinado backgroundColor;<br /> atributo somente leitura shortColor;<br /> atributo não assinado shortColor; Color;<br /> <br /> // Size<br /> const. short SIZE_DEFAULT não assinado = 0 ;<br /> const. short SIZE_SMALL = 1 ;<br /> const. short SIZE_MEDIUM não assinado = 2 ;<br /> const short SIZE_LARGE = 3 ;<br /> <br /> atributo readonly de tamanho curto não assinado;<br /> <br /> // FontEdge<br /> const. curta não assinado FONT_EDGE_DEFAULT = 0 ;<br /> const. short FONT_EDGE_NONE = 1 ;<br /> const. curta não assinado FONT_EDGE_RAISED = 2 ;<br /> const não assinado curto FONT_EDGE_DEPRESSED = 3 ;<br /> const short não assinado FONT_EDGE_UNIFORM = 4 ;<br /> const short não assinado FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const short não assinado FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> atributo readonly short fontEdge não assinado;<br /> <br /> // Font<br /> const short FONT_DEFAULT = 0 ;<br /> const short não assinado FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned Fshort ONT_SMALL_CAPITALS = 6 ;<br /> atributo readonly atributo unsigned short font;<br /> atributo readonly atributo unsigned short fontOpacity;<br /> atributo readonly não assinado backgroundOpacity;<br /> atributo readonly shortOpacity;<br /> atributo readonly só de leitura unsigned short DEFAULT_OPACITY;&lt;a &gt; };<br /></p> </td> 
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
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource, long resourceId,<br /> ItemLoaderListener listener, <br /> MediaPlayerItemConfig config);<br /> void cancel();<br /> atributo readonly MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Novo para o 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallback Func;<br /> }</p> </td> 
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
   <td><p>interface MediaPlayerItem {<br /> atributo somente leitura MediaResource;<br /> atributo readonly long resourceId;<br /> atributo readonly boolean live;<br /> <br /> atributo readonly boolean hasAlternateAudio;<br /> atributo readonly AudioTrackList audioTracks;<br /> atributo somente leitura Track seletedAudioTrack;<br /> void selectAudioTrack(faixa AudioTrack); <br /> <br /> atributo somente leitura booleano hasClosedCaptions;<br /> atributo somente leitura ClosedCaptionsTrackList closedCaptionsTracks;<br /> atributo somente leitura ClosedCaptionsTrack seletedCaptionsTrack;<br /> void selectClosedCaptionsTrack( a13/&gt; faixa ClosedCaptionsTrack); <br /> <br /> atributo somente leitura boolean hasTimedMetadata;<br /> atributo somente leitura TimedMetadataList timedMetadata;<br /> atributo somente leitura boolean dynamic;<br /> <br /> atributo somente leitura isProtected; a20/&gt; atributo somente leitura perfis ProfileList DRMMetadataInfoList drmMetadataInfos;<br /> atributo somente leitura  ProfileList;<br /> Perfil de atributo somente leitura seletedProfile;<br /> <br /> atributo somente leitura trickPlaySupported;&lt;a2 Atributo somente leitura FloatArray availablePlaybackRates;<br /> atributo somente leitura float seletedPlaybackRate;<br /> <br /> <br /> atributo somente leitura MediaPlayer mediaPlayer;<br /> atributo somente leitura Configuração MediaPlayerItemConfig;&lt;a 31/&gt; };<br /><br /><br /><br /></p> </td> 
   <td><p>interface MediaPlayerItem {<br /> atributo somente leitura MediaResource;<br /> atributo readonly long resourceId;<br /> atributo readonly boolean live;<br /> <br /> atributo readonly boolean hasAlternateAudio;<br /> atributo readonly AudioTrackList audioTracks;<br /> atributo AudioTrack seletedAudioTrack;<br /> <br /> <br /> atributo somente leitura boolean hasClosedCaptions;<br /> atributo somente leitura ClosedCaptionsTrackList ccTracks;<br /> atributo ClosedCaptionsTrack seletedCCTrack;<br /> <br /> <br /> <br /> atributo somente leitura boolean hasTimedMetadata;<br /> atributo somente leitura TimedMetadataList timedMetadata;<br /> atributo somente leitura boolean dynamic;<br /> <br /> atributo somente leitura isProtected; O atributo somente leitura <br /> DRMMetadataInfoList drmMetadataInfos;<br /> atributos somente leitura ProfileList perfis;<br /> <br /> <br /> atributo somente leitura trickPlaySupported;<br /> atributo somente leitura Atributo inválido t32Array availablePlaybackRates;<br /> <br /> atributo somente leitura StringList adTags;<br /> <br /> atributo somente leitura MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
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
   <td><p>interface Track<br /> {<br /> atributo somente leitura Nome DomString;<br /> atributo somente leitura Idioma DomString;<br /> atributo somente leitura default booleano;<br /> atributo somente leitura autoSelect;<br /> }; </p> </td> 
   <td>Novo para o 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Track<br /> {<br /> atributo somente leitura Nome DomString; //FromTrack<br /> atributo somente leitura Linguagem DomString;//FromTrack<br /> atributo somente leitura padrão booleano; // Do Track<br /> atributo somente leitura booleano autoSelect;//FromTrack<br /> <br /> atributo somente leitura int pid não assinado;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> atributo somente leitura Nome DomString;<br /> atributo somente leitura Linguagem DomString; <br /> atributo somente leitura padrão booleano;<br /> atributo somente leitura booliano autoSelect;<br /> atributo somente leitura booleano forçado;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> atributo readonly de comprimento longo não assinado;<br /> getter AudioTrack (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Track<br /> {<br /> atributo somente leitura Nome DomString; //FromTrack<br /> atributo somente leitura Linguagem DomString;//FromTrack<br /> atributo somente leitura padrão booleano; // FromTrack<br /> atributo somente leitura boolean autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VEB TT_CAPTIONS = 2;<br /> atributo readonly atributo unsigned short serviceType;<br /> atributo readonly boolean forced;<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> atributo somente leitura Nome DomString;<br /> atributo somente leitura Linguagem DomString;<br /> atributo somente leitura padrão booleano;<br /> <br /> <br /> atributo somente leitura booleano ativo;<br /> <br /> <br /> &lt;a10&gt; <br /> <br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> atributo somente leitura de comprimento longo não assinado;<br /> getter ClosedCaptionsTrack(índice longo não assinado);<br /> };</p> </td> 
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
   <td><p>perfil de interface<br /> {<br /> atributo readonly unsigned int width;<br /> atributo readonly só de leitura unsigned int height;<br /> atributo readonly unsigned int bit Rate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: Nenhuma alteração para 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> atributo somente leitura de comprimento longo não assinado;<br /> Perfil getter (índice longo não assinado);<br /> };</p> </td> 
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
   <td><p>interface DRMMetadataInfo<br /> { <br /> atributo somente leitura metadados DRMMetadata;<br /> atributo readonly prefetchTimestamp;<br /> atributo readonly TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Nenhuma alteração para 2.0</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> atributo readonly de comprimento longo não assinado;<br /> getter DRMMetadataInfo(índice longo não assinado);<br /> };</p> </td> 
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
   <td><p>interface Version<br /> {<br /> atributo somente leitura versão DomString;<br /> atributo somente leitura Descrição DomString;<br /> atributo somente leitura long major;<br /> atributo somente leitura long minor;<br /> atributo somente leitura revisão longa;<br /> atributo somente leitura longa apiVersion;<br /> };</p> </td> 
   <td><p>interface Version<br /> {<br /> atributo somente leitura versão DomString;<br /> atributo somente leitura Descrição DomString;<br /> atributo somente leitura DomString major;<br /> atributo somente leitura DomString minor;<br /> atributo somente leitura DomString revisão;<br /> atributo somente leitura DomString apiVersion;&lt;a7/ };<br /></p> </td> 
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
   <td><p>interface TimeRange<br /> {<br /> atributo readonly unsigned long begin;<br /> atributo readonly só de leitura unsigned long end;<br /> atributo readonly de longa duração não assinada;<br /> };</p> </td> 
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
   <td><p>interface QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> atributo somente leitura DeviceInformation deviceInformation;<br /> atributo somente leitura PlaybackInformation playbackInformation;<br /> };</p> </td> 
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
   <td><p>interface DeviceInformation<br /> {<br /> atributo somente leitura DomString os;<br /> <br /> <br /> <br /> atributo somente leitura DomString id;<br /> atributo somente leitura int DPI;<br /> atributo somente leitura int heightPixels;&lt;a8/9&gt; atributo somente leitura int widthPixels;&lt;a/&gt; atributo somente leitura: requestToKeyFrame;<br /> };<br /><br /></p> </td> 
   <td><p>interface DeviceInformation<br /> {<br /> atributo somente leitura DomString os;<br /> atributo somente leitura int sdk;<br /> atributo somente leitura Modelo DomString;<br /> atributo somente leitura fabricante DomString;<br /> atributo somente leitura DomString id;<br /> atributo somente leitura int DPI;<br /> atributo int heightPixels;<br /> atributo somente leitura int widthPixels;<br /> <br /> };</p> </td> 
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
   <td><p>interface LoadInfo<br /> {<br /> atributo somente leitura url DomString;<br /> atributo somente leitura int size;<br /> atributo somente leitura downloadDuration;<br /> atributo somente leitura int periodIndex;<br /> atributo somente leitura mediaDuration;<br /> atributo readonly short TRACK_TYPE_FRAGMENT;&lt;a7&gt; atributo readonly short TRACK_TYPE_TRACK;<br /> atributo readonly short TRACK_TYPE_MANIFEST;<br /> atributo readonly short type;<br /> atributo readonly DomString trackName;<br /> atributo readonly DomString trackType;<br /> atributo readonly int trackIndex;<br /> };<br /></p> </td> 
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
   <td><p>visualização da interface<br /> {<br /> atributo somente leitura não assinado short x;<br /> atributo somente leitura não assinado short y;<br /> atributo somente leitura não assinado largura curta;<br /> atributo somente leitura de altura curta não assinada;<br /> <br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### PlaybackInformation {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>1.3 APIs</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo readonly timeToFirstByte;<br /> atributo readonly timeToLoad;<br /> atributo readonly timeToStart;<br /> atributo readonly timeToFail;<br /> atributo readonly atributo int totalSecondsPlayed;<br /> atributo somente leitura em totalSecondsSpent;<br /> atributo somente leitura duplo frameRate;<br /> atributo somente leitura int droppedFrameCount;<br /> atributo somente leitura intBandwidth;<br /> atributo somente leitura int bitrate;<br /> atributo readonly bufferTime;<br /> atributo only int bufferLength;<br /> atributo somente leitura em emptyBufferCount;<br /> atributo readonly bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo readonly timeToFirstByte;<br /> atributo readonly timeToLoad;<br /> atributo readonly timeToStart;<br /> atributo readonly timeToFail;<br /> atributo readonly atributo int totalSecondsPlayed;<br /> atributo somente leitura em totalSecondsSpent;<br /> atributo somente leitura duplo frameRate;<br /> atributo somente leitura int droppedFrameCount;<br /> <br /> atributo somente leitura em bitrate;<br /> atributo somente leitura bufferTime;<br /> atributo somente leitura int bufferLength; atributo readonly em emptyBufferCount;<br /> bufferingTime do duplo de atributo somente leitura;<br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte da Adobe Primetime](https://helpx.adobe.com/support/primetime.html).
