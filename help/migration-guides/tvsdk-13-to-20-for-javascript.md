---
title: Conversão do TVSDK - 1.3 para 2.0 para JavaScript
description: Muitas assinaturas de método e nomes de elementos de API foram alterados para 2.0. Revise essas tabelas para ver todos os detalhes de alteração da API.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
exl-id: 4b251e26-cee6-4d96-bb55-6c47195da4d0
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---

# Conversão do TVSDK - 1.3 para 2.0 para JavaScript {#tvsdk-conversion-to-for-javascript}

Muitas assinaturas de método e nomes de elementos de API foram alterados para 2.0. Revise essas tabelas para ver todos os detalhes de alteração da API.

## Implementar funções de retorno de chamada no JavaScript {#implement-callback-functions-in-javascript}

Comentários na documentação do método sugerem a assinatura para retornos de chamada que você precisa implementar.

Para JavaScript, a sintaxe da API é baseada na Web ID. Para uma interface TVSDK, os nomes dos métodos são chamados de *methodName*(). Para os métodos a serem implementados pelo aplicativo, um atributo de leitura/gravação chamado *methodName* CallbackFunc é adicionado à interface e seu aplicativo deve defini-lo para apontar para uma função que implemente o método. Por exemplo:

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

## Alterações no elemento da API do fluxo de trabalho de publicidade para 2.0 {#advertising-workflow-api-element-changes-for}

Essas tabelas comparam os elementos da API do workflow de publicidade do TVSDK do JavaScript entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* TimedMetadata
* ModoDeSinalizaçãoAnúncio
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Posicionamento
* Oportunidade
* Reserva
* Linha do tempo / Item da linha do tempo / Marcador da linha do tempo
* AdBreak
* Ad/AdAsset/AdClick/AdList/AdAssetList/AdBannerAsset
* AdBreakTimelineItem/AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* OperaçãoDaLinhaDoTempo
* AdBreakPlacement
* ConfiguraçõesAuditoria

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>: interface TimedMetadata {<br /> const METADATA_TYPE_TAG curto sem sinal = 0 ; <br /> const METADATA_TYPE_ID3 abreviado sem sinal = 1 ; <br /> tipo curto sem sinal de atributo readonly; <br /> atributo somente leitura por muito tempo;<br /> id DomString de atributo somente leitura;<br /> nome DomString de atributo somente leitura;<br /> conteúdo DomString de atributo somente leitura; <br /> atributo somente leitura Metadados de objeto;<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const METADATA_TYPE_TAG curto sem sinal = 0 ;<br /> const METADATA_TYPE_ID3 abreviado sem sinal = 1 ;<br /> atributo readonly unsigned short metadataType;<br /> atributo somente leitura por muito tempo;<br /> id longa do atributo somente leitura;<br /> nome DomString de atributo somente leitura;<br /> <br /> atributo somente leitura Metadados de objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface TimedMetadataList {<br /> comprimento longo não assinado do atributo readonly;<br /> getter TimedMetadata(índice longo sem sinal);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ModoDeSinalizaçãoAnúncio {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>Interface AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const unsigned short MODE_SERVER_MAP , <br /> const. sem sinal MODE_CUSTOM_RANGES <br /> };</p> </td> 
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
   <td><p>Interface AdvertisingMetadata { <br /> Atributo ModoAdSignaling; <br /> Atributo AdBreakWatchedPolicy adBreakAsWatched; <br /> atributo booleano livePreroll; <br /> atributo booleano delayAdLoading ; <br /> };</p> </td> 
   <td>Essa funcionalidade foi fornecida por<p>MetadataKeys::ADVERTISING_METADATA</p> chave.</td> 
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
   <td><p>Interface CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const TYPE_REPLACE_RANGE curto sem sinal; <br /> tipo curto sem sinal de atributo; <br /> atributo booleano adjustSeekPosition; <br /> atributo TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> começar longo sem sinal do atributo; <br /> fim longo não assinado do atributo readonly; <br /> Atributo de longa duração sem sinal; <br /> attribute replaceDuration longo e sem sinal; <br /> };</p> </td> 
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
   <td><p>Posicionamento da interface { <br /> const TYPE_MID_ROLL curto não assinado; <br /> const TYPE_PRE_ROLL curto sem sinal; <br /> const unsigned short TYPE_POST_ROLL; <br /> const TYPE_SERVER_MAP curto sem sinal; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> tipo curto sem sinal de atributo readonly; <br /> atributo somente leitura por muito tempo; <br /> longa duração do atributo readonly; <br /> const não assinado MODE_DEFAULT; <br /> const sem sinal MODE_INSERT; <br /> const não assinado MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const sem sinal MODE_MARK; <br /> const não assinado MODE_FREE_REPLACE; <br /> modo curto sem sinal do atributo readonly; <br /> intervalo de TimeRange do atributo somente leitura; <br /> };</p> </td> 
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
   <td><p>Oportunidade de interface { <br /> id DomString de atributo somente leitura; <br /> inserção de atributo somente leitura; <br /> configurações de Object do atributo somente leitura; <br /> atributo somente leitura Object customParameters; <br /> }; </p> </td> 
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
   <td><p>Interface Reservation { <br /> intervalo de TimeRange do atributo somente leitura; <br /> retenção longa de atributo somente leitura; <br /> }; </p> </td> 
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
   <td><p><strong>Linha do tempo</strong>: Linha de tempo da interface <br /> { atributo somente leitura TimelineMarkerList timelineMarkers; <br /> atributo somente leitura TimelineItemList timelineItems; <br /> double convertToLocalTime( double time); <br /> double convertToVirtualTime( tempo duplo); <br /> };</p> </td> 
   <td><p>Linha do tempo da interface {<br /> atributo somente leitura TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>ItemDaLinhaDoTempo</strong>: interface TimelineItem :<br /> TimelineMarker {<br /> id longa do atributo somente leitura; <br /> atributo somente leitura TimeRange virtualRange; <br /> atributo somente leitura TimeRange localRange; <br /> atributo somente leitura booleano observado; <br /> atributo somente leitura booleano temporário; <br /> }; </p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>MarcadorDeLinhaDoTempo</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> atributo somente leitura de tempo duplo;<br /> duração dupla do atributo readonly;<br /> };</p> </td> 
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
   <td><p>interface AdBreak {<br /> <br /> <br /> <br /> duração dupla do atributo readonly;<br /> anúncios AdList de atributos somente leitura;<br /> <br /> <br /> atributo somente leitura AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> atributo somente leitura de tempo duplo;<br /> atributo somente leitura replaceDuration duplo;<br /> <br /> duração dupla do atributo readonly;<br /> atributo somente leitura AdList adList;<br /> <br /> dados DomString de atributo somente leitura;<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad/AdAsset/AdClick/AdList/AdAssetList/AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Anúncio</strong>: interface Ad {<br /> atributo somente leitura AdAsset primaryAsset;<br /> atributo somente leitura AdAssetList companionAssets;<br /> <br /> duração dupla do atributo readonly;<br /> id DomString de atributo somente leitura;<br /> const abreviado sem sinal ADTYPE_LINEAR = 0 ;<br /> const short ADTYPE_NONLINEAR sem sinal = 1 ;<br /> <br /> adType curto sem sinal de atributo readonly;<br /> atributo somente leitura AdInsertionType adInsertionType; <br /> <br /> atributo somente leitura booleano clicável; <br /> atributo somente leitura booleano isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {<br /> atributo somente leitura AdAsset primaryAsset;<br /> atributo somente leitura AdAssetList companionAssets;<br /> <br /> duração dupla do atributo readonly;<br /> id DomString de atributo somente leitura;<br /> const abreviado sem sinal ADTYPE_LINEAR = 0 ;<br /> const short ADTYPE_NONLINEAR sem sinal = 1 ;<br /> <br /> tipo curto sem sinal de atributo readonly;<br /> atributo somente leitura AdInsertionType insertionType; <br /> atributo somente leitura Rastreador de objeto;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdAsset {<br /> id DomString de atributo somente leitura;<br /> duração dupla do atributo readonly;<br /> atributo de somente leitura MediaResource;<br /> atributo somente leitura AdClick adClick;<br /> atributo somente leitura Metadados de objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdClick {<br /> id DomString de atributo somente leitura;<br /> título DomString de atributo somente leitura;<br /> url DomString de atributo somente leitura;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdList {<br /> comprimento longo não assinado do atributo readonly;<br /> getter Ad(índice longo sem sinal);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Sem alteração para 2.0)</td> 
   <td><p>interface AdAssetList {<br /> comprimento longo não assinado do atributo readonly;<br /> getter AdAsset(índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interface AdBannerAsset : AdAsset<br /> {<br /> atributo somente leitura em largura;<br /> atributo somente leitura em altura;<br /> atributo somente leitura DomString staticUrl;<br /> altura de DomString de atributo somente leitura;<br /> largura de DomString de atributo somente leitura;<br /> };</p> </td> 
   <td> Novidades do 2.0</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem/AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : TimelineItem { <br /> atributo somente leitura AdBreak adBreak; <br /> itens AdTimelineItemList de atributo somente leitura; <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : TimelineItem { <br /> atributo somente leitura AdBreak adBreak; <br /> atributo Ad ad somente leitura; <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { <br /> comprimento longo não assinado do atributo readonly; <br /> getter AdBreakTimelineItem (índice de log não assinado); <br /> };</p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AdBreakPolicy {<br /> atributo somente leitura curto AD_BREAK_POLICY_SKIP;<br /> atributo somente leitura curto AD_BREAK_POLICY_PLAY;<br /> atributo somente leitura AD_BREAK_POLICY_REMOVE curto;<br /> atributo somente leitura curto AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> atributo somente leitura curto AD_BREAK_POLICY_SKIP;<br /> atributo somente leitura curto AD_BREAK_POLICY_PLAY;<br /> atributo somente leitura AD_BREAK_POLICY_REMOVE curto;<br /> atributo somente leitura curto AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ..</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ..<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_NEVER;<br /> ..</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> atributo somente leitura curto AD_POLICY_PLAY;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; atributo somente leitura curto AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo somente leitura curto AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> .. <br /> atributo somente leitura curto AD_POLICY_PLAY;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo somente leitura curto AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> atributo somente leitura curto AD_POLICY_SKIP_AD_BREAK;<br /> ..</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> atributo somente leitura curto AD_POLICY_MODE_PLAY;<br /> atributo somente leitura curto AD_POLICY_MODE_SEEK;<br /> atributo somente leitura curto AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ..<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> atributo somente leitura curto AD_POLICY_MODE_SEEK;<br /> atributo somente leitura curto AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> atributo somente leitura AdTimelineItem adTimelineItem;<br /> atributo somente leitura currentTime duplo;<br /> atributo readonly double seekToTime;<br /> taxa dupla de atributo somente leitura;<br /> modo curto do atributo readonly; //AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakPlacementList <br /> adBreakPlacements;<br /> atributo Ad ad somente leitura;<br /> atributo somente leitura currentTime duplo;<br /> atributo readonly double seekToTime;<br /> taxa dupla de atributo somente leitura;<br /> modo curto do atributo readonly; //AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> Atributo Objeto selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> Atributo Objeto selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> Atributo Objeto selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> Atributo Objeto selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> Atributo Objeto selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> Atributo Objeto selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> Atributo Objeto selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo (adPolicyInfo);<br /> */<br /> Atributo Objeto selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### OperaçãoDaLinhaDoTempo {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface TimelineOperation { <br /> inserção de atributo somente leitura ; <br /> };</p> </td> 
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
   <td><p>interface AdBreakPlacement : TimelineOperation {<br /> atributo somente leitura AdBreak adBreak;<br /> inserção de atributo somente leitura; // De TimelineOperation<br /> atributo somente leitura de tempo duplo;<br /> duração dupla do atributo readonly;<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> atributo somente leitura AdBreak adBreak;<br /> inserção de atributo somente leitura;<br /> atributo somente leitura de tempo duplo;<br /> duração dupla do atributo readonly;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ConfiguraçõesAuditoria {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface AuditudeSettings : AdvertisingMetadata { <br /> attribute DomString zoneId; <br /> attribute DomString mediaId; <br /> attribute DomString defaultMediaId ; <br /> domínio DomString do atributo ; <br /> attribute Objeto targetInfo ; <br /> Atributo Objeto customParameters ; <br /> attribute Boolean creativePackingEnabled ;<br /> atributo booleano showStaticBanners ;<br /> };</p> </td> 
   <td>A funcionalidade foi fornecida pela chave MetadataKeys::AUDITUDE_METADATA_KEY.</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API de personalização para 2.0 {#customization-api-element-changes-for}

Essas tabelas comparam os elementos da API de personalização do TVSDK do JavaScript entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* MediaPlayerItemConfig
* ContentFactory
* NetworkConfiguration

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> atributo StringList subscribeTags;<br /> <br /> atributo StringList adTags;<br /> <br /> <br /> atributo AdSignalingMode adSignalingMode;<br /> Atributo CustomRangeMetadata customRangeMetadata;<br /> atributo NetworkConfiguration networkConfiguration;<br /> atributo AdvertisingMetadata advertisingMetadata;<br /> atributo booleano useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> <br /> <br /> <br /> atributo StringList adTags;<br /> atributo StringList subscribedTags;<br /> atributo MediaPlayerClientFactory clientFactory;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem);<br /> */<br /> Atributo Objeto retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem);<br /> */<br /> Atributo Objeto retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> atributo booleano forceNativeNetworking;<br /> atributo booleano useRedirectionUrl;<br /> atributo Object cookieHeader;<br /> atributo booleano readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> atributo booleano useCookieHeaderForAllRequests;<br /> atributo int readLimit;<br /> };</p> </td> 
   <td>Na versão 1.3, parte dessa funcionalidade era fornecida pelo MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API do DRM para 2.0 {#drm-api-element-changes-for}

Essas tabelas comparam os elementos da API DRM para o TVSDK do JavaScript entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* Inicialização do fluxo de trabalho DRM
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* MetadadosDRM
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### Inicialização do fluxo de trabalho DRM {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>O aplicativo precisa chamar AdobePSDK.initiateDRMWorkflow para iniciar o fluxo de trabalho de DRM. Sem essa chamada, os vídeos DRM não serão reproduzidos.<p>interface AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>A inicialização foi feita internamente e nenhuma chamada explícita foi necessária.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| APIs 2.0 | APIs 1.3 |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| Nenhuma alteração para 2.0. | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| Nenhuma alteração para 2.0. | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANÔNIMO = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### MetadadosDRM {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0.</td> 
   <td><p>Metadados de DRMM de interface<br /> {<br /> atributo somente leitura DomString serverUrl;<br /> atributo somente leitura DomString licenseId;<br /> políticas DRMPolicyArray de atributo somente leitura; <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo readonly em playbackPeriodInSeconds;<br /> atributo readonly long playbackStartDate;<br /> atributo readonly long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo somente leitura em periodInSeconds;<br /> atributo somente leitura int startDate;<br /> atributo somente leitura int endDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0.</td> 
   <td><p>interface DRMLicense {<br /> atributo somente leitura Uint8Array bytes;<br /> atributo somente leitura Date licenseStartDate;<br /> atributo somente leitura Date licenseEndDate;<br /> atributo somente leitura Date offlineStorageStartDate;<br /> atributo somente leitura Date offlineStorageEndDate; <br /> atributo somente leitura DomString serverUrl;<br /> atributo somente leitura DomString licenseID;<br /> atributo somente leitura DomString policyID;<br /> atributo somente leitura DRMPlaybackTimeWindow playbackTimeWindow;<br /> atributo somente leitura Object customProperties;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
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
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMPolicy<br /> {<br /> atributo somente leitura DomString authenticationDomain;<br /> atributo somente leitura DRMAuthenticationMethod authenticationMethod;<br /> <br /> atributo somente leitura DomString displayName;<br /> atributo somente leitura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {<br /> atributo somente leitura DomString authDomain;<br /> atributo somente leitura DRMAuthenticationMethod authMethod;<br /> atributo somente leitura DomString dispName;<br /> atributo somente leitura DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(metadados de metadados de DRMMetadata, <br /> definição DRMAcquireLicenseSettings, <br /> DRMAquireLicenseListener);<br /> void acquisitionPreviewLicense(metadados de metadados de DRMM, <br /> DRMAquireLicenseListener);<br /> void authenticate(metadados DRMMetadata, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> Usuário DomString, <br /> Senha DomString, <br /> DRMAuthenticateListener);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array, DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener ouvinte);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> commitImmediately booleano,<br /> DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> Metadados DRMMetadata, <br /> DomString authenticationDomain, <br /> Uint8Token de matriz, <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(metadados de metadados de DRMMetadata, <br /> definição DRMAcquireLicenseSettings, <br /> EventContext (eventContext);<br /> void acquisitionPreviewLicense(metadados de metadados de DRMM, <br /> EventContext (eventContext);<br /> void authenticate(metadados DRMMetadata, <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> Usuário DomString, <br /> Senha DomString, <br /> EventContext (eventContext);<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array (matriz, EventContext (eventContext);<br /> void initialize(EventContext eventContext);<br /> atributo long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext (eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext (eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> commitImmediately booleano,<br /> EventContext (eventContext);<br /> void setAuthenticationToken(<br /> Metadados DRMMetadata, <br /> DomString authenticationDomain, <br /> Uint8Token de matriz, <br /> EventContext (eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext (eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> público:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t menor, <br /> const psdkutils:: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protegido:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando ocorre um erro durante um dos métodos assíncronos do DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMOperationCompleteListener : <br /> DRMErrorListener público {<br /> público:<br /> virtual void onDRMOperationComplete() = 0;<br /> <br /> protegido:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>Quando a inicialização do DRM estiver concluída.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>Quando a ação joinLicenseDomain() é concluída com êxito.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>Quando a ação leaveLicenseDomain() é concluída com sucesso.</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>Quando a ação resetDRM() é concluída com êxito.</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>Quando a ação setAuthenticationTokenSet() é concluída com sucesso.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>Quando a ação storeLicenseBytes() é concluída com êxito.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAuthenticateListener : <br /> DRMErrorListener público {<br /> público:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Quando a chamada do método DRMManager::authenticate é bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAquireLicenseListener: <br /> DRMErrorListener público {<br /> público:<br /> virtual void onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionPreviewLicense é bem-sucedida.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionLicense é bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMReturnLicenseListener: <br /> DRMErrorListener público {<br /> público:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned ) = 0;<br /> <br /> protegido:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Quando a chamada do método DRMManager::returnLicense é bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Alterações genéricas no elemento da API de reprodução para 2.0 {#generic-playback-api-element-changes-for}

Essas tabelas comparam os elementos da API de reprodução genérica entre o JavaScript TVSDK 1.3 e 2.0.

Tabelas neste tópico:

* MediaResource
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* FormatoDeTexto
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> url DomString de atributo; <br /> tipo curto sem sinal de atributo;<br /> Atributo Metadados do objeto;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> url DomString de atributo;<br /> tipo de atributo DomString;<br /> Atributo Metadados do objeto;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( posição dupla);<br /> void play();<br /> void pause();<br /> void seek (posição dupla);<br /> void seekToLocal( posição dupla);<br /> void reset();<br /> void release();<br /> anular replaceCurrentItem(MediaPlayerItem item);<br /> void replaceCurrentResource(MediaResource, <br /> MediaPlayerItemConfig); <br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> <br /> atributo somente leitura TimeRange playbackRange;<br /> atributo somente leitura TimeRange seekableRange;<br /> atributo somente leitura currentTime duplo;<br /> atributo somente leitura double localTime;<br /> atributo somente leitura TimeRange bufferedRange;<br /> atributo somente leitura DRMManager drmManager;<br /> atributo somente leitura MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> <br /> const não assinado curto PLAYER_STATUS_INITIALIZED;<br /> const sem sinal short PLAYER_STATUS_PREPARING;<br /> const sem sinal short PLAYER_STATUS_PREPARED;<br /> const sem sinal short PLAYER_STATUS_PLAYING;<br /> const não assinado curto PLAYER_STATUS_PAUSED;<br /> const não assinado curto PLAYER_STATUS_SEEKING;<br /> const não assinado curto PLAYER_STATUS_COMPLETE;<br /> const sem sinal short PLAYER_STATUS_ERROR;<br /> const sem sinal short PLAYER_STATUS_RELEASED;<br /> <br /> atributo somente leitura status curto não assinado;<br /> <br /> Atributo volume curto sem sinal;<br /> Atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> const unsigned short VISIBLE; //Para visibilidade CC<br /> const unsigned short INVISIBLE; //Para visibilidade CC<br /> Atributo ccVisibility curta não assinada;<br /> atributo TextFormat ccStyle;<br /> atributo somente leitura PlaybackMetrics playbackMetrics;<br /> <br /> taxa dupla do atributo;<br /> atributo MediaPlayerView;<br /> linha do tempo do atributo somente leitura;<br /> atributo double currentTimeUpdateInterval; <br /> // configuração não será compatível com 2.0<br /> };</p> </td> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void prepareToPlay( int position);<br /> void play();<br /> void pause();<br /> void seek( int position);<br /> void seekToLocalTime( int position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo somente leitura TimeRange playbackRange;<br /> atributo somente leitura TimeRange seekableRange;<br /> atributo somente leitura currentTime duplo;<br /> atributo somente leitura double localTime;<br /> atributo somente leitura TimeRange bufferedRange;<br /> atributo somente leitura DRMManager drmManager;<br /> atributo somente leitura MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const não assinado curto PLAYER_STATE_IDLE;<br /> const não assinado curto PLAYER_STATE_INITIALIZING;<br /> const não assinado curto PLAYER_STATE_INITIALIZED;<br /> const não assinado curto PLAYER_STATE_PREPARING;<br /> const não assinado curto PLAYER_STATE_PREPARED;<br /> const sem sinal short PLAYER_STATE_PLAYING;<br /> const não assinado curto PLAYER_STATE_PAUSED;<br /> const não assinado curto PLAYER_STATE_SEEKING;<br /> const não assinado curto PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const não assinado curto PLAYER_STATE_RELEASED;<br /> const não assinado curto PLAYER_STATUS_SUSPENDED;<br /> estado curto não assinado do atributo readonly;<br /> <br /> Atributo volume curto sem sinal;<br /> Atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> readonly unsigned short VISIBLE; //Para visibilidade CC<br /> somente leitura não assinado curto INVISÍVEL; //Para visibilidade CC<br /> Atributo ccVisibility curta não assinada;<br /> atributo TextFormat ccStyle;<br /> atributo somente leitura PlaybackMetrics playbackMetrics;<br /> atributo MediaPlayerConfig mediaPlayerConfig;<br /> taxa dupla do atributo;<br /> atributo MediaPlayerView;<br /> linha do tempo do atributo somente leitura;<br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const não assinado curto PLAYER_STATUS_IDLE;<br /> const não assinado curto PLAYER_STATUS_INITIALIZING;<br /> const não assinado curto PLAYER_STATUS_INITIALIZED;<br /> const sem sinal short PLAYER_STATUS_PREPARING;<br /> const sem sinal short PLAYER_STATUS_PREPARED;<br /> const sem sinal short PLAYER_STATUS_PLAYING;<br /> const não assinado curto PLAYER_STATUS_PAUSED;<br /> const não assinado curto PLAYER_STATUS_SEEKING;<br /> const não assinado curto PLAYER_STATUS_COMPLETE;<br /> const sem sinal short PLAYER_STATUS_ERROR;<br /> const sem sinal short PLAYER_STATUS_RELEASED;<br /> const não assinado curto PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Eventos compatíveis com o MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 Nome do evento</th> 
   <th>Interface 2.0</th> 
   <th> </th> 
   <th>1.3 Nome do evento</th> 
   <th>Interface 1.3</th> 
  </tr> 
  <tr> 
   <td><p>(excluído para 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>preparado</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>Quando um item do reprodutor de mídia é atualizado.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>atualizado</p> <p>Quando o reprodutor de mídia atualizou a mídia com êxito.</p> </td> 
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
   <td>linha do tempoAtualizada</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>CronogramaAtualizado</td> 
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
   <td>EventoTempo</td> 
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
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>EventoTempo</td> 
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
   <td>reservationReached</td> 
   <td>EventoReserva</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>EventoDeDetentorDaLinhaDoTempo</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSelected</td> 
   <td>EventoTaxaReprodução</td> 
   <td> </td> 
   <td>rateSelected</td> 
   <td>EventoTaxaReprodução</td> 
  </tr> 
  <tr> 
   <td>ratePlaying</td> 
   <td>EventoTaxaReprodução</td> 
   <td> </td> 
   <td>ratePlaying</td> 
   <td>EventoTaxaReprodução</td> 
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
   <td><p>Novidades do 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Quando o perfil de reprodução muda.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Novidades do 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>posiçãoDeBuscaAjustada<br /> Quando a posição de busca é ajustada devido a regras internas ou externas.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novidades do 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> Quando um item do reprodutor de mídia é atualizado. Para certos fluxos que contêm faixas de áudio detectáveis somente no momento da reprodução, esse evento é disparado quando novas faixas de áudio estão disponíveis.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades do 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>legendasAtualizadas <br /> Quando um item do reprodutor de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades do 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> Quando um item do reprodutor de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades do 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> Quando um item do reprodutor de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso acontece, certas características da mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades do 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Enviado quando eventos cronometrados são gerados.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Novidades do 2.0</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> attribute unsigned short abrPolicy;<br /> atributo unsigned int initialBitRate;<br /> atributo unsigned int minBitRate;<br /> atributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface BufferControlParameters<br /> {<br /> atributo double initialBufferTime;<br /> atributo double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> atributo double initialBufferTime;<br /> atributo double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### FormatoDeTexto {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface TextFormat<br /> {<br /> // Cor<br /> const COLOR_DEFAULT curto sem sinal = 0 ;<br /> const COLOR_BLACK curto sem sinal = 1 ;<br /> const COLOR_GRAY curto sem sinal = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const abreviado sem sinal COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const abreviado sem sinal COLOR_DARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const COLOR_BRIGHT_GREEN curto sem sinal = 10 ;<br /> const abreviado sem sinal COLOR_DARK_BLUE = 11 ;<br /> const COLOR_BLUE curto sem sinal = 12 ;<br /> const COLOR_BRIGHT_BLUE curto sem sinal = 13 ;<br /> const abreviado sem sinal COLOR_DARK_YELLOW = 14 ;<br /> const COLOR_YELLOW curto sem sinal = 15 ;<br /> const COLOR_BRIGHT_YELLOW curto sem sinal = 16 ;<br /> const abreviado sem sinal COLOR_DARK_MAGENTA = 17 ;<br /> const COLOR_MAGENTA curto sem sinal = 18 ;<br /> const COLOR_BRIGHT_MAGENTA curto sem sinal = 19 ;<br /> const abreviado sem sinal COLOR_DARK_CYAN = 20 ;<br /> const COLOR_CYAN curto sem sinal = 21 ;<br /> const COLOR_BRIGHT_CYAN curto sem sinal = 22 ;<br /> <br /> fontColor curto sem sinal de atributo somente leitura;<br /> atributo readonly unsigned short backgroundColor;<br /> atributo readonly unsigned short fillColor;<br /> atributo readonly unsigned short edgeColor;<br /> <br /> // Tamanho<br /> const sem sinal short SIZE_DEFAULT = 0 ;<br /> const sem sinal short SIZE_SMALL = 1 ;<br /> const sem sinal short SIZE_MEDIUM = 2 ;<br /> const sem sinal short SIZE_LARGE = 3 ;<br /> <br /> tamanho curto sem sinal de atributo somente leitura;<br /> <br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const sem sinal FONT_EDGE_DEPRESSED curto = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const não assinado FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> atributo somente leitura unsigned short fontEdge;<br /> <br /> // Fonte<br /> const unsigned short_FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const não assinado curto FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const FONT_SMALL_CAPITALS curto sem sinal = 6 ;<br /> fonte curta não assinada do atributo somente leitura;<br /> atributo readonly unsigned short fontOpacity;<br /> atributo readonly unsigned short backgroundOpacity;<br /> atributo readonly unsigned short fillOpacity;<br /> atributo readonly unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> void load(Recurso do MediaResource, ID de recurso longo,<br /> Ouvinte ItemLoaderListener, <br /> MediaPlayerItemConfig ) ;<br /> void cancel();<br /> atributo somente leitura MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Novo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>Novo para 2.0</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API das características de mídia para 2.0 {#media-characteristics-api-element-changes-for}

Essas tabelas comparam os elementos de API das características de mídia do TVSDK C++ entre as versões 1.3 e 2.0.

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
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {<br /> atributo de somente leitura MediaResource;<br /> atributo readonly long resourceId;<br /> atributo somente leitura booleano live;<br /> <br /> atributo somente leitura booleano hasAlternateAudio;<br /> atributo somente leitura AudioTrackList audioTracks;<br /> atributo somente leitura AudioTrack selecionadoAudioTrack;<br /> void selectAudioTrack(AudioTrack track); <br /> <br /> atributo somente leitura booleano hasClosedCaptions;<br /> atributo somente leitura ClosedCaptionsTrackList closedCaptionsTracks;<br /> atributo somente leitura ClosedCaptionsTrack seletedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack); <br /> <br /> atributo de somente leitura booleano hasTimedMetadata;<br /> atributo somente leitura TimedMetadataList timedMetadata;<br /> atributo somente leitura booleano dinâmico;<br /> <br /> atributo somente leitura booleano isProtected;<br /> atributo somente leitura DRMMetadataInfoList drmMetadataInfos;<br /> perfis ProfileList de atributos somente leitura;<br /> atributo somente leitura Perfil selecionado;<br /> <br /> atributo somente leitura de booleano trickPlaySupported;<br /> atributo somente leitura FloatArray availablePlaybackRates;<br /> atributo somente leitura float seletedPlaybackRate;<br /> <br /> <br /> atributo somente leitura MediaPlayer mediaPlayer;<br /> atributo somente leitura MediaPlayerItemConfig config;<br /> };</p> </td> 
   <td><p>interface MediaPlayerItem {<br /> atributo de somente leitura MediaResource;<br /> atributo readonly long resourceId;<br /> atributo somente leitura booleano live;<br /> <br /> atributo somente leitura booleano hasAlternateAudio;<br /> atributo somente leitura AudioTrackList audioTracks;<br /> Atribuir AudioTrack selecionadoAudioTrack;<br /> <br /> <br /> atributo somente leitura booleano hasClosedCaptions;<br /> atributo somente leitura ClosedCaptionsTrackList ccTracks;<br /> atributo ClosedCaptionsTrack seletedCCTrack;<br /> <br /> <br /> <br /> atributo de somente leitura booleano hasTimedMetadata;<br /> atributo somente leitura TimedMetadataList timedMetadata;<br /> atributo somente leitura booleano dinâmico;<br /> <br /> atributo somente leitura booleano isProtected;<br /> atributo somente leitura DRMMetadataInfoList drmMetadataInfos;<br /> perfis ProfileList de atributos somente leitura;<br /> <br /> <br /> atributo somente leitura de booleano trickPlaySupported;<br /> atributo somente leitura Int32Array availablePlaybackRates;<br /> <br /> atributo somente leitura StringList adTags;<br /> <br /> atributo somente leitura MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track/AudioTrack/ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> nome DomString de atributo somente leitura;<br /> linguagem DomString de atributo somente leitura;<br /> padrão booleano do atributo readonly;<br /> atributo somente leitura booleano autoSelect;<br /> }; </p> </td> 
   <td>Novo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Track<br /> {<br /> atributo somente leitura DomString name; //FromTrack<br /> linguagem DomString de atributo somente leitura;//FromTrack<br /> padrão booleano do atributo readonly; // Da trilha<br /> atributo somente leitura booleano autoSelect;//FromTrack<br /> <br /> atributo readonly unsigned int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> nome DomString de atributo somente leitura;<br /> linguagem DomString de atributo somente leitura; <br /> padrão booleano do atributo readonly;<br /> atributo somente leitura booleano autoSelect;<br /> atributo somente leitura booleano forçado;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> comprimento longo não assinado do atributo readonly;<br /> getter AudioTrack (índice longo sem sinal);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Track<br /> {<br /> atributo somente leitura DomString name; //FromTrack<br /> linguagem DomString de atributo somente leitura;//FromTrack<br /> padrão booleano do atributo readonly; // FromTrack<br /> atributo somente leitura booleano autoSelect;//FromTrack<br /> <br /> <br /> const não assinado SERVICE_608_CAPTIONS = 0;<br /> const curto SERVICE_708_CAPTIONS não assinado = 1;<br /> const não assinado SERVICE_WEB_VTT_CAPTIONS = 2;<br /> atributo readonly unsigned short serviceType;<br /> atributo somente leitura booleano forçado;<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> nome DomString de atributo somente leitura;<br /> linguagem DomString de atributo somente leitura;<br /> padrão booleano do atributo readonly;<br /> <br /> <br /> atributo de somente leitura booleano ativo;<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface ClosedCaptionsTrackList<br /> {<br /> comprimento longo não assinado do atributo readonly;<br /> getter ClosedCaptionsTrack(índice longo sem sinal);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Perfil {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Perfil: nenhuma alteração para 2.0</td> 
   <td><p>Perfil da interface<br /> {<br /> atributo somente leitura unsigned int width;<br /> altura int do atributo sem sinal de somente leitura;<br /> atributo readonly unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList: sem alteração para 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> comprimento longo não assinado do atributo readonly;<br /> Getter Profile(índice longo sem sinal);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>: nenhuma alteração para 2.0</td> 
   <td><p>interface DRMMetadataInfo<br /> { <br /> metadados DRMMetadata de atributo somente leitura;<br /> atributo readonly long prefetchTimestamp;<br /> atributo somente leitura TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: nenhuma alteração para 2.0</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> comprimento longo não assinado do atributo readonly;<br /> getter DRMMetadataInfo(índice longo não assinado);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Mapeando Erros de C++ a Exceções em Diferentes Idiomas {#mapping-c-errors-to-exceptions-in-different-languages}

Você pode mapear códigos de erro do C++ para exceções em diferentes idiomas.

A PSDK do C++ tem uma política de &quot;não lançamento&quot; para suas APIs. A maioria dos métodos de API retorna um valor PSDKErrorCode para indicar se o método foi executado com êxito. Os erros assíncronos são notificados por meio dos eventos de erro.

O ActionScript e o JAVA PSDK têm uma política diferente. A maioria dos erros lançará um ArgumentError ou IllegalStateException para indicar que a parte síncrona do método não pôde ser executada. Essas exceções não são detectadas e o código do aplicativo é responsável por lidar com elas. Normalmente, eles carregam informações úteis sobre por que a chamada do método falhou. Por exemplo, se o comando prepareToPlay for chamado em um estado inválido, a seguinte exceção será lançada:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

O ActionScript/JAVA também lança exceções de construtores para indicar que algum objeto interno foi criado incorretamente. Essas exceções são tratadas internamente e não são propagadas para o aplicativo. As exceções serão incluídas em uma notificação de aviso enviada ao aplicativo

Por exemplo, se nenhum arquivo de mídia válido foi encontrado para a resposta de anúncio recebida, nenhum objeto de ativo de anúncio ou anúncio válido pode ser criado. Como resultado, nenhum anúncio é colocado na linha do tempo e uma notificação NotificationEvent.OperationFailed é enviada.

Códigos de erro ou de aviso recebidos de forma assíncrona do Mecanismo de vídeo de Adobe (AVE) são enviados para o aplicativo como eventos normais. O evento de notificação contém todos os códigos de erro recebidos e metadados adicionais, como URL, identificador de recurso, identificador e assim por diante. Se o erro for grave e a reprodução da mídia atual não puder continuar, o MediaPlayer fará a transição para o status ERROR e o retorno de chamada onStatusChanged ou o evento MediaPlayerStatusChanged.STATUS_CHANGED será despachado. Se a reprodução continuar, um evento de notificação normal será despachado.

<table> 
 <tbody> 
  <tr> 
   <th>Erro de C++ (PSDKError Code)</th> 
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
   <td>Exceção com código = 1, descrição = "INVALID_ARGUMENT" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Exceção com código = 2, descrição = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Exceção com código = 3, descrição = "ILLEGAL_STATE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>InterfaceNãoEncontradaECI</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 4, descrição = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 5, descrição = "CREATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperationName</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 5, descrição = "CREATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 7, descrição = "DATA_NOT_AVAILABLE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 8, descrição = "SEEK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 9, descrição = "UNSUPPORTED_FEATURE" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 10, descrição = "RANGE_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 11, descrição = "CODEC_NOT_SUPPORTED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 12, descrição = "MEDIA_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 13, descrição = "NETWORK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error ou MediaPlayerNotification.Warning</td> 
   <td>MediaError ou NotificationEvent</td> 
   <td>Exceção com código = 14, descrição = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 15, descrição = "INVALID_SEEK_TIME" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 16, descrição = "AUDIO_TRACK_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 17, descrição = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 18, descrição = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 19, descrição = "GENERIC_ERROR" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 200, descrição = "PLAYBACK_OPERATION_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Exceção com código = 201, descrição = "NATIVE_WARNING" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Exceção com código = 202, descrição = "AD_RESOLVER_FAILED" e additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Alterações nos elementos de API do utilitário e do assistente para 2.0 {#utility-and-helper-api-element-changes-for}

Essas tabelas comparam os elementos da API do utilitário e do assistente para o TVSDK do JavaScript entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* Versão
* Intervalo de tempo
* QOSProvider
* DeviceInformation
* LoadInfo
* Exibir
* InformaçõesDeReprodução

### Versão {#version}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>versão da interface<br /> {<br /> versão DomString de atributo somente leitura;<br /> descrição do atributo DomString somente leitura;<br /> atributo long major somente leitura;<br /> atributo long minor somente leitura;<br /> revisão longa do atributo somente leitura;<br /> apiVersion longa de atributo somente leitura;<br /> };</p> </td> 
   <td><p>versão da interface<br /> {<br /> versão DomString de atributo somente leitura;<br /> descrição do atributo DomString somente leitura;<br /> atributo DomString major somente leitura;<br /> atributo DomString minor somente leitura;<br /> revisão DomString de atributo somente leitura;<br /> atributo somente leitura DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Intervalo de tempo {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>TimeRange da interface<br /> {<br /> início longo não assinado do atributo readonly;<br /> fim longo não assinado do atributo readonly;<br /> longa duração do atributo readonly unsigned;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>QOSProvider de interface<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> atributo somente leitura DeviceInformation deviceInformation;<br /> atributo somente leitura PlaybackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DeviceInformation {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>DeviceInformation de interface<br /> {<br /> atributo somente leitura DomString os;<br /> <br /> <br /> <br /> id DomString de atributo somente leitura;<br /> atributo somente leitura int densityDPI;<br /> atributo somente leitura em heightPixels;<br /> atributo somente leitura em widthPixels;<br /> atributo somente leitura do booleano seekToKeyFrame;<br /> };</p> </td> 
   <td><p>DeviceInformation de interface<br /> {<br /> atributo somente leitura DomString os;<br /> atributo somente leitura int sdk;<br /> modelo DomString de atributo somente leitura;<br /> fabricante do atributo DomString somente leitura;<br /> id DomString de atributo somente leitura;<br /> atributo somente leitura int densityDPI;<br /> atributo somente leitura em heightPixels;<br /> atributo somente leitura em widthPixels;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface LoadInfo<br /> {<br /> url DomString de atributo somente leitura;<br /> atributo somente leitura em tamanho;<br /> atributo somente leitura double downloadDuration;<br /> atributo somente leitura int periodIndex;<br /> atributo somente leitura mediaDuration duplo;<br /> atributo somente leitura abreviado TRACK_TYPE_FRAGMENT;<br /> atributo somente leitura short TRACK_TYPE_TRACK;<br /> atributo somente leitura short TRACK_TYPE_MANIFEST;<br /> tipo curto de atributo somente leitura;<br /> atributo DomString trackName somente leitura;<br /> atributo DomString trackType somente leitura;<br /> atributo somente leitura int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Exibir {#view}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>Visualização da interface<br /> {<br /> atributo somente leitura unsigned short x;<br /> atributo somente leitura unsigned short y;<br /> largura curta não assinada do atributo somente leitura;<br /> altura curta sem sinal do atributo readonly;<br /> <br /> void setSize(largura curta sem sinal, altura curta sem sinal);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### InformaçõesDeReprodução {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo somente leitura double timeToFirstByte;<br /> atributo somente leitura double timeToLoad;<br /> atributo somente leitura double timeToStart;<br /> atributo somente leitura double timeToFail;<br /> atributo somente leitura em totalSecondsPlayed;<br /> atributo somente leitura int totalSecondsSpent;<br /> atributo somente leitura double frameRate;<br /> atributo readonly int droppedFrameCount;<br /> atributo somente leitura em perceptívelLargura de banda;<br /> atributo somente leitura int bitrate;<br /> atributo somente leitura double bufferTime;<br /> atributo somente leitura int bufferLength;<br /> atributo readonly int emptyBufferCount;<br /> atributo somente leitura double bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo somente leitura double timeToFirstByte;<br /> atributo somente leitura double timeToLoad;<br /> atributo somente leitura double timeToStart;<br /> atributo somente leitura double timeToFail;<br /> atributo somente leitura em totalSecondsPlayed;<br /> atributo somente leitura int totalSecondsSpent;<br /> atributo somente leitura double frameRate;<br /> atributo readonly int droppedFrameCount;<br /> <br /> atributo somente leitura int bitrate;<br /> atributo somente leitura double bufferTime;<br /> atributo somente leitura int bufferLength;<br /> atributo readonly int emptyBufferCount;<br /> atributo somente leitura double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
