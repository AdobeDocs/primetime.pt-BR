---
title: Conversão de TVSDK - 1.3 para 2.0 para JavaScript
description: Muitas assinaturas de método e nomes de elemento da API foram alteradas para 2.0. Revise essas tabelas para ver todos os detalhes de alteração da API.
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---


# Conversão de TVSDK - 1.3 para 2.0 para JavaScript {#tvsdk-conversion-to-for-javascript}

Muitas assinaturas de método e nomes de elemento da API foram alteradas para 2.0. Revise essas tabelas para ver todos os detalhes de alteração da API.

## Implementar funções de retorno de chamada no JavaScript {#implement-callback-functions-in-javascript}

Os comentários na documentação do método sugerem a assinatura para retornos de chamada que você precisa implementar.

Para JavaScript, a sintaxe da API é baseada na ID da Web. Para uma interface TVSDK, os nomes dos métodos são chamados de *methodName*(). Para que os métodos sejam implementados pelo seu aplicativo, um atributo de leitura/gravação chamado *methodName* CallbackFunc é adicionado à interface e seu aplicativo deve defini-lo para apontar para uma função que implementa o método. Por exemplo:

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

Essas tabelas comparam os elementos da API do fluxo de trabalho de publicidade para o TVSDK do JavaScript entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* TimedMetadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* Posicionamento
* Oportunidade
* Reserva
* Linha do tempo / Item da linha do tempo / Marcador de linha do tempo
* AdBreak
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* OperaçãoLinhaTempo
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
   <td><p> <strong>TimedMetadata</strong>: interface TimedMetadata {<br /> const short METADATA_TYPE_TAG = 0 ;  <br /> const short METADATA_TYPE_ID3 não assinado = 1 ;  <br /> tipo abreviado não assinado do atributo somente leitura;  <br /> atributo somente leitura por tempo longo; atributo somente <br /> leitura ID DomString; nome DomString do atributo somente <br /> leitura; conteúdo DomString do atributo somente <br /> leitura;  <br /> Metadados do Objeto do atributo somente leitura; <br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br /> const.unsigned short METADATA_TYPE_TAG = 0 ;<br /> const.unsigned short METADATA_TYPE_ID3 = 1 ;<br /> atributo somente leitura unsigned short metadataType;<br /> atributo somente leitura longo tempo;<br /> id de atributo somente leitura longa;<br /> atributo somente leitura DomString;<br /> <br /> atributo somente leitura Metadados de objeto;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>: (Sem alterações para 2.0)</td> 
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
   <td><p>Interface AdSignalingMode { <br /> const short MODE_DEFAULT não assinado, <br /> const unsigned short MODE_MANIFEST_CUES , <br /> const unsigned short MODE_SERVER_MAP , <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>Isso substitui a chave MetadataKeys::MANIFEST_CUES .</td> 
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
   <td><p>Interface AdvertisingMetadata { <br /> atributo AdSignalingMode modo; Atributo <br /> AdBreakWatchedPolicy adBreakAsWatched; <br /> atributo booleano livePreroll; <br /> atributo booleano delayAdLoading ; <br /> };</p> </td> 
   <td>Essa funcionalidade foi fornecida por<p>MetadataKeys::ADVERTISING_METADATA</p> key.</td> 
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
   <td><p>Interface CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> atributo de tipo curto não assinado; Atributo <br /> booleano adaptSeekPosition; <br /> atributo TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br /> atributo long begin não assinado; <br /> atributo somente leitura de fim longo não assinado; <br /> atributo de longa duração não assinado; <br /> atributo replaceDuration longo não assinado; <br /> };</p> </td> 
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
   <td><p>Posicionamento da Interface { <br /> const short TYPE_MID_ROLL não assinado; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> atributo somente leitura tipo curto não assinado; <br /> atributo somente leitura por muito tempo; <br /> atributo somente leitura de longa duração; <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const short MODE_REPLACE não assinado; <br /> const short MODE_DELETE não assinado; <br /> const short MODE_MARK não assinado; <br /> const short MODE_FREE_REPLACE não assinado; <br /> atributo somente leitura no modo curto não assinado; <br /> atributo somente leitura Intervalo de tempo; <br /> };</p> </td> 
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
   <td><p>interface Oportunidade { <br /> atributo somente leitura DomString id; <br /> colocação de disposição de atributo somente leitura; <br /> configurações de Objeto de atributo somente leitura; <br /> atributo somente leitura Object customParameters; <br /> }; </p> </td> 
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
   <td><p>reserva de interface { <br /> intervalo de tempo do atributo somente leitura; <br /> atributo somente leitura de retenção longa; <br /> }; </p> </td> 
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
   <td><p><strong>Linha do tempo</strong>: linha do tempo da interface  <br /> { atributo somente leitura TimelineMarkerList timelineMarkers;  <br /> atributo somente leitura TimelineItemList timelineItems;  <br /> double conversionToLocalTime (tempo duplo);  <br /> double conversionToVirtualTime (tempo duplo);  <br /> };</p> </td> 
   <td><p>linha do tempo da interface {<br /> atributo somente leitura TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>Item</strong> da Linha do Tempo: interface TimelineItem:<br /> TimelineMarker {<br /> readonly attribute long id;  <br /> atributo somente leitura TimeRange virtualRange;  <br /> atributo readonly TimeRange localRange;  <br /> atributo somente leitura booleano observado;  <br /> atributo somente leitura booleano temporário;  <br /> }; </p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>: (Sem alterações para 2.0)</td> 
   <td><p>interface TimelineMarker {<br /> atributo somente leitura tempo duplo;<br /> atributo somente leitura duração dupla;<br /> };</p> </td> 
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
   <td><p>interface AdBreak {<br /> <br /> <br /> <br /> atributo somente leitura dupla duração;<br /> atributo somente leitura Anúncios AdList;<br /> <br /> <br /> atributo somente leitura AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> atributo somente leitura tempo duplo;<br /> atributo somente leitura double replaceDuration;<br /> <br /> atributo somente leitura duração dupla;<br /> atributo somente leitura AdList adList;<br /> <br /> atributo somente leitura DomString data;<br /> <br /> }; </p> </td> 
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
   <td><p> <strong>Anúncio</strong>: interface Ad {atributo <br /> somente leitura AdAsset primaryAsset; atributo somente <br /> leitura AdAssetList companionAssets; atributo somente <br /> <br /> leitura dupla duração; atributo somente <br /> leitura DomString id; <br /> const short ADTYPE_LINEAR = 0 ; <br /> const unsigned short ADTYPE_NONLINEAR = 1; atributo somente <br /> <br /> leitura tipo de anúncio curto não assinado; <br /> somente leitura Atributo AdInsertionType adInsertionType;  <br /> <br /> atributo somente leitura, booleano clicável;  <br /> o atributo somente leitura booleano isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {<br /> atributo somente leitura AdAsset primaryAsset;<br /> atributo somente leitura AdAssetList companionAssets;<br /> <br /> atributo somente leitura de duração dupla;<br /> atributo somente leitura DomString id;<br /> const curta não assinado ADTYPE_LINEAR = 0 ;<br /> const não-short ADTYPE NONLINEAR = 1 ;<br /> <br /> atributo somente leitura tipo curto não assinado;<br /> atributo somente leitura AdInsertionType insertionType; <br /> atributo somente leitura Rastreador de objetos;<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>: (Sem alterações para 2.0)</td> 
   <td><p>interface AdAsset {<br /> atributo somente leitura DomString id;<br /> atributo somente leitura dupla duração;<br /> atributo somente leitura recurso MediaResource;<br /> atributo somente leitura AdClick adClick;<br /> metadados do objeto de atributo somente leitura;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>: (Sem alterações para 2.0)</td> 
   <td><p>interface AdClick {<br /> atributo somente leitura DomString id;<br /> atributo somente leitura DomString title;<br /> atributo somente leitura DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>: (Sem alterações para 2.0)</td> 
   <td><p>interface AdList {<br /> atributo somente leitura de comprimento longo não assinado;<br /> getter Ad(índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>: (Sem alterações para 2.0)</td> 
   <td><p>interface AdAssetList {<br /> atributo somente leitura de comprimento longo não assinado;<br /> getter AdAsset(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>: interface AdBannerAsset : AdAsset<br /> {<br /> atributo somente leitura na largura; atributo somente <br /> leitura na altura; atributo somente <br /> leitura DomString staticUrl; altura de DomString do atributo somente <br /> leitura; largura de DomString do atributo somente <br /> leitura; <br /> };</p> </td> 
   <td> Novidades na versão 2.0</td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>: interface AdBreakTimelineItem : TimelineItem { atributo  <br /> somente leitura AdBreak adBreak;  <br /> itens AdTimelineItemList do atributo somente leitura;  <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>: interface AdTimelineItem : TimelineItem { atributo  <br /> somente leitura AdBreak adBreak;  <br /> anúncio de atributo somente leitura;  <br /> }; </p> </td> 
   <td> (Novo para 2.0)</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>: interface AdBreakTimelineItemList { atributo  <br /> readonly unsigned long length;  <br /> get AdBreakTimelineItem (índice ng não assinado);  <br /> };</p> </td> 
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
   <td><p>interface AdBreakPolicy {<br /> atributo somente leitura curto AD_BREAK_POLICY_SKIP;<br /> atributo somente leitura curto AD_BREAK_POLICY_PLAY;<br /> atributo somente leitura curto AD_BREAK_POLICY_REMOVE;<br /> atributo somente leitura curto AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> atributo somente leitura curto AD_BREAK_POLICY_SKIP;<br /> atributo somente leitura curto AD_BREAK_POLICY_PLAY;<br /> atributo somente leitura curto AD_BREAK_POLICY_REMOVE;<br /> atributo somente leitura curto AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_NEVER;&lt;a3/ &gt; };<br /> </p> </td> 
   <td><p> ...<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_ON_END;<br /> atributo somente leitura curto AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> atributo somente leitura curta AD_POLICY_PLAY;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN; Atributo somente leitura curto AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> atributo somente leitura curto AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> .. <br /> atributo somente leitura curto AD_POLICY_PLAY;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> atributo somente leitura curto AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> atributo somente leitura curto AD_POLICY_SKIP_TO_NEXT_AD_IN_BREIN AK;<br /> atributo somente leitura curto AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> atributo somente leitura curta AD_POLICY_MODE_PLAY;<br /> atributo somente leitura curta AD_POLICY_MODE_SEEK;<br /> atributo somente leitura curta AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {atributo somente leitura abreviado AD_POLICY_MODE_PLAY;<br /> atributo somente leitura curta AD_POLICY_MODE_SEEK;<br /> atributo somente leitura abreviado AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> atributo somente leitura AdTimelineItem adTimelineItem;<br /> atributo somente leitura currentTime duplo;<br /> atributo somente leitura atributo taxa dupla;<br /> atributo somente leitura modo curto; //AdPolicyMode<br /> };<br /></p> </td> 
   <td><p>interface AdPolicyInfo {<br /> atributo somente leitura AdBreakPlacementList <br /> adBreakPlacments;<br /> atributo somente leitura Ad;<br /> atributo somente leitura currentTime;<br /> atributo somente leitura Modo curto; //AdPolicyMode<br /> };<br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /*<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForAdBreakCallbackFunc;<br /> /* a6/&gt; * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBred akCallbackFunc;<br /> };<br /></p> </td> 
   <td><p>interface AdPolicySelector {<br /> /*<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForAdBreakFuncCallback;<br /> /* a6/&gt; * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectAdBreaksToPlayCallback;<br /> /**<br /> * Ad dPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> atributo Object selectWatchedPolicyForAdBred akCallback;<br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### OperaçãoLinhaTempo {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>API 2.0</th> 
   <th>API 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface TimelineOperation { <br /> colocação de atributo somente leitura; <br /> };</p> </td> 
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
   <td><p>interface AdBreakPlacement : Linha do tempo Operação {<br /> atributo somente leitura AdBreak adBreak;<br /> colocação de disposição do atributo somente leitura; // Da TimelineOperation<br /> atributo somente leitura de tempo duplo;<br /> atributo somente leitura de duração dupla;<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {<br /> atributo somente leitura AdBreak adBreak;<br /> atributo somente leitura Inserção de disposição;<br /> atributo somente leitura tempo duplo;<br /> atributo somente leitura duração dupla;<br /> };</p> </td> 
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
   <td><p>interface AuditudeSettings : AdvertisingMetadata { <br /> atributo DomString zoneId; <br /> atributo DomString mediaId; <br /> atributo DomString defaultMediaId ; <br /> atributo Domínio DomString ; <br /> atributo Object targettingInfo ; Atributo <br /> Object customParameters ; <br /> atributo Boolean creativePackaingEnabled ;<br /> atributo Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>A funcionalidade foi fornecida pela chave MetadataKeys::AUDITUDE_METADATA_KEY.</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API de personalização para 2.0 {#customization-api-element-changes-for}

Essas tabelas comparam os elementos da API de personalização para o TVSDK do JavaScript entre as versões 1.3 e 2.0.

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
   <td><p>Interface MediaPlayerItemConfig {<br /> atributo ContentFactory adFactory;<br /> atributo StringList subscribeTags;<br /> <br /> atributo StringList adTags;<br /> <br /> atributo AdSignalingMode adRangeSignaling;<br /> atributo Custom Metadados customRangeMetadata;<br /> atributo NetworkConfiguration NetworkConfiguration;<br /> atributo AdvertisingMetadata advertisingMetadata;<br /> atributo Booleano useHardwareDecoder;<br /> };<br /></p> </td> 
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
   <td><p>interface ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem item);<br /> */<br /> atributo Object retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem item);<br /> */<br /> atributo Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
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
   <td><p>interface NetworkConfiguration<br /> atributo booleano forceNativeNetworking;<br /> atributo booleano useRedirectUrl;<br /> atributo Object cookieHeader;<br /> atributo booleano readSetCookieHeader;<br /> atributo int masterUpdateInterval; Atributo <br /> booleano useCookieHeaderForAllRequests;<br /> atributo int readLimit;<br /> };<br /></p> </td> 
   <td>No 1.3, parte dessa funcionalidade foi fornecida pelo MetadataKeys</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API DRM para 2.0 {#drm-api-element-changes-for}

Essas tabelas comparam os elementos da API de DRM para TVSDK do JavaScript entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* Inicialização do fluxo de trabalho DRM
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* Política DRMP
* DRMManager

### Inicialização do fluxo de trabalho DRM {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>O aplicativo precisa chamar AdobePSDK.initiateDRMWorkflow para iniciar o fluxo de trabalho do DRM. Sem esta chamada, os vídeos de DRM não serão reproduzidos.<p>interface AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> boolean privacy Mode On);<br /> };</p> </td> 
   <td>A inicialização foi feita internamente e nenhuma chamada explícita era necessária.</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| APIs 2.0 | APIs 1.3 |
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
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0.</td> 
   <td><p>interface DRMMetadata<br /> {<br /> atributo somente leitura DomString serverUrl;<br /> atributo somente leitura DomString licenseId;<br /> políticas DRMPolicyArray; <br /> };</p> </td> 
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
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo somente leitura em playbackPeriodInSeconds;<br /> atributo somente leitura playbackStartDate;<br /> atributo somente leitura long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> atributo somente leitura em periodInSeconds;<br /> atributo somente leitura em startDate;<br /> atributo somente leitura em endDate;<br /> };</p> </td> 
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
   <td><p>interface DRMLicense {<br /> atributo somente leitura Bytes Uint8Array;<br /> atributo somente leitura Data licençaStartDate;<br /> atributo somente leitura Data licençaEndDate;<br /> atributo somente leitura Data offlineStorageStartDate;<br /> atributo somente leitura Data offlineStorageEndDate; <br /> atributo somente leitura DomString serverUrl;<br /> atributo somente leitura DomString licenseID;<br /> atributo somente leitura DomString policyID;<br /> atributo somente leitura DRMPlaybackTimeWindow playbackTimeWindow;<br /> atributo somente leitura Object customProperties;<br /> }; </p> </td> 
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
   <td><p>interface DRMPolicy<br /> {<br /> atributo somente leitura DomString authDomain;<br /> atributo somente leitura DRMAuthenticationMethod authMethod;<br /> atributo somente leitura DomString dispName;<br /> atributo somente leitura DRMLicenseDomain licenseDomain;<br /> }</p> </td> 
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
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(DRMMetadata metadata, <br /> DRMAcquireLicenseSettings, <br /> DRMAquireLicenseListener listener);<br /> void acquisitionPreviewLicense(DRMMetadata metadata, <br /> DRMAquire Ouvinte do enseListener);<br /> void authentication(Metadados DRMMetadata, <br /> URL DomString,<br /> DomString &amp;authenticationDomain, <br /> Usuário DomString, <br /> Senha DomString, <br /> Ouvinte DRMAuthenticateListener);&lt;a 11/&gt; <br /> DRMMetadata createMetadataFromBytes(<br /> Array array, DRMErrorListener listener);<br /> void initialize(DRMOperationCompleteListener listener listener);<br /> atributo long maxOperation Time;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener listener listener);<br /> voidLicense Domain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener listener);<br /> <br /> void resetDRM(DRMOperationCompleteListener listener listener);<br /> void returnLicense(Dom String serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> booleano commitImediatamente,<br /> DRMReturnLicenseListener listener);<br /> void setAuthenticationToken(&lt;a0 32/&gt; Metadados DRMMetadata, <br /> DomString authenticationDomain, <br /> Token Uint8Array, <br /> DRMOperationCompleteListener listener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, &lt;a3 7/&gt; DRMOperationCompleteListener (ouvinte);<br /> };<br /><br /><br /></p> </td> 
   <td><p>interface DRMManager : EventTarget {<br /> void acquisitionLicense(DRMMetadata metadata, <br /> DRMAcquireLicenseSettings, <br /> EventContext eventContext);<br /> void acquisitionPreviewLicense(DRMMetadata metadata, <br /> EventContext eventContext);<br /> void authentication(Metadata DRMMetadata, <br /> URL DomString,<br /> DomString &amp;authenticationDomain, <br /> Usuário DomString, <br /> Senha DomString, <br /> EventContext eventContext);<br /> <br /> DRMM metadados createMetadataFromBytes(<br /> Matriz Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> attribute long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> booleano forceRefresh, <br /> EventContext eventContext);<br /> void allowLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> Context eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, &lt;a2 booleano commitImediatamente,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> Metadados DRMMetadata, <br /> DomString authenticationDomain, <br /> Token Uint8Array, &lt;a EventContext (eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };<br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils: PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl) = 0;<br /> <br /> protegido:<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>Quando ocorre um erro durante um dos métodos assíncronos do DRMManger.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMOperationCompleteListener : <br /> DRMErrorListener público {<br /> público:<br /> vazio virtual em DRMOperationComplete() = 0;<br /> <br /> protegido:<br /> virtual ~DRMOperationCompleteListener() {}<br /> };</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEEvent</p> <p>Quando a inicialização do DRM estiver concluída.</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEEvent</p> <p>Quando a ação joinLicenseDomain() é concluída com êxito.</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEEvent</p> <p>Quando a ação allowLicenseDomain() é concluída com êxito.</p> </li> 
     <li>kEventDRMResetCompletePSDKEEvent<p>/ PSDKEEvent</p> <p>Quando a ação resetDRM() é concluída com êxito.</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEEvent</p> <p>Quando a ação setAuthenticationTokenSet() é concluída com êxito.</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEEvent</p> <p>Quando a ação storeLicenseBytes() é concluída com êxito.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAuthenticateListener : <br /> DRMErrorListener público {<br /> público:<br /> valor virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken) = 0;<br /> <br /> protegido:<br /> Virtual DRMA AuthenticateListener() {}<br /> }</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>Quando a chamada do método DRMManager::authentication é bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMAquireLicenseListener: <br /> DRMErrorListener público {<br /> público:<br /> vazio virtual onLicenseAcquired(const DRMLicense*) = 0;<br /> <br /> protegido:<br /> virtual ~DRMAquireLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionLicense é bem-sucedida.</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>Quando a chamada do método DRMManager::acquisitionLicense é bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>classe DRMReturnLicenseListener: <br /> DRMErrorListener público {<br /> público:<br /> vazio virtual onLicenseReturnComplete(uint32_t numReturn ) = 0;<br /> <br /> protegido:<br /> virtual ~DRMReturnLicenseListener() {}<br /> };</p> </td> 
   <td>Evento / Interface / Descrição 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>Quando a chamada do método DRMManager::returnLicense é bem-sucedida.</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API de reprodução genérica para 2.0 {#generic-playback-api-element-changes-for}

Essas tabelas comparam os elementos da API de reprodução genérica entre o JavaScript TVSDK 1.3 e 2.0.

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
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br /> atributo DomString url; <br /> atributo de tipo curto não assinado;<br /> atributo Metadados de objeto;<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> atributo DomString url;<br /> atributo DomString tipo;<br /> atributo Object metadata;<br /> <br /> <br /> <br /> <br /> <br />  };</p> </td> 
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
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void preparationToPlay( posição dupla);<br /> void play();<br /> void pause();<br /> void search( posição dupla);<br /> void searchToLocal( posição dupla);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem(item MediaPlayerItem);<br /> void replaceCurrentResource(MediaResource source, <br /> MediaPlayerItemConfig config); <br /> void drop();<br /> void restore();<br /> void notifyClick();<br /> <br /> atributo somente leitura TimeRange playbackRange;<br /> atributo somente leitura TimeRange;<br /> atributo somente leitura currentTime;<br /> atributo somente leitura double localTime;<br /> atributo somente leitura TimeRange bufferedRange;<br /> atributo somente leitura DRMManager drmManager;<br /> atributo somente leitura MediaPlayerItem currentItem;<br /> <br /> / PlayerStatus<br /> <br /> <br /> const short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const short PLAYER_STATUS_PREPARED não assinado;<br /> const curta não assinado PLAYER_STATUS_PLAYING;<br /> const short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const PLAYER_STATUS_ERROR;<br /> abreviado não assinado PLAYER_STATUS_RELEASED;<br /> <br /> atributo somente leitura status curto não assinado;<br /> atributo <br /> volume curto não assinado;<br /> atributo ABRControl Parâmetros abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> const short VISIBLE não assinado; //Para CC visibility<br /> const unsigned short INVISIBLE; //Para atributo de visibilidade CC<br /> curto ccVisibility sem sinal;<br /> atributo TextFormat ccStyle;<br /> atributo somente leitura PlaybackMetrics playbackMetrics;<br /> <br /> atributo taxa dupla;<br /> atributo MediaPlayerView;<br /> atributo somente leitura Linha do tempo;<br /> atributo currentTimeUpdateInterval duplo; <br /> // definir isso não será suportado para 2.0<br /> };</p> </td> 
   <td><p>interface MediaPlayer : EventTarget<br /> {<br /> void preparationToPlay( int position);<br /> void play();<br /> void pause();<br /> void search( int position);<br /> void searchToLocalTime( int position);<br /> void reset();<br /> void release();8/&gt; void replaceCurrentItem(MediaResource source);<br /> <br /> <br /> <br /> <br /> <br /> <br /> atributo somente leitura TimeRange playbackRange;<br /> atributo somente leitura TimeRange; <br /> atributo somente leitura currentTime duplo;<br /> atributo somente leitura localTime duplo;<br /> atributo somente leitura TimeRange bufferedRange;<br /> atributo somente leitura DRMManager drmManager;<br /> atributo somente leitura MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br /> const short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned PLAYER_STATE_PREPARING;<br /> const short PLAYER_STATE_PREPARED sem sinal;<br /> const short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const short PLAYER_STATE_SEEEE KING;<br /> const short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED;<br /> atributo somente leitura de estado curto não assinado;<br /> <br /> atributo de volume curto não assinado;<br /> atributo ABRControlParameters abrControlParameters;<br /> atributo BufferControlParameters bufferControlParameters;<br /> <br /> somente leitura não assinado breve VISÍVEL; //Para CC visibility<br /> readonly unsigned short INVISIBLE; //Para atributo de visibilidade CC<br /> curto ccVisibility sem sinal;<br /> atributo TextFormat ccStyle;<br /> atributo somente leitura PlaybackMetrics playbackMetrics;<br /> atributo MediaPlayerConfig mediaPlayerConfig;<br /> taxa dupla de atributo; a49/&gt; atributo MediaPlayerView view;<br /> atributo somente leitura Linha do tempo;<br /> <br /> <br /> };<br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br /> const. curta não assinado PLAYER_STATUS_IDLE;<br /> const. curta não assinada PLAYER_STATUS_INITIALIZING;<br /> const. curta não assinada PLAYER_STATUS_INITIALIZED;<br /> const ER_STATUS_PREPARING;<br /> const não assinado short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const short não assinado PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>(Novo para 2.0)</td> 
  </tr> 
 </tbody> 
</table>

#### Eventos compatíveis com MediaPlayer {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>Nome do evento 2.0</th> 
   <th>Interface 2.0</th> 
   <th> </th> 
   <th>1.3 Nome do evento</th> 
   <th>Interface 1.3</th> 
  </tr> 
  <tr> 
   <td><p>(suprimido para 2.0)</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>preparado</td> 
   <td>Evento</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>Quando um item do reprodutor de mídia é atualizado.</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>atualizado</p> <p>Quando o reprodutor de mídia tiver atualizado a mídia com êxito.</p> </td> 
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
   <td>timelineUpdated</td> 
   <td>Evento</td> 
   <td> </td> 
   <td>TmelineUpdated</td> 
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
   <td>size</td> 
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
   <td><p>Novidades na versão 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> Quando o perfil de reprodução muda.</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>Novidades na versão 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>searchPositionAjusted<br /> Quando a posição de busca é ajustada devido a regras internas ou externas.</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>Novidades na versão 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> Quando um item do reprodutor de mídia é atualizado. Para certos fluxos que contêm trilhas de áudio que são detectáveis somente no momento da reprodução, esse evento é disparado quando novas trilhas de áudio estão disponíveis.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades na versão 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>legendasAtualizadas <br /> Quando um item do reprodutor de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso ocorre, certas características de mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades na versão 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br /> Quando um item de reprodutor de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso ocorre, certas características de mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades na versão 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> Quando um item do reprodutor de mídia é atualizado. Para fluxos ao vivo/lineares, o cliente deve atualizar periodicamente o recurso de mídia para detectar o novo conteúdo disponível. Quando isso ocorre, certas características de mídia podem mudar.</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>Novidades na versão 2.0</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Enviado quando eventos cronometrados são gerados.</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>Novidades na versão 2.0</p> </td> 
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
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> atributo abrPolicy não assinado Atributo;<br /> não assinado em initialBitRate;<br /> atributo não assinado em minBitRate;<br /> atributo não assinado em maxBitRate;<br /> const não assinado short DEFAULT_ABR_INITIAL_BITRATE;<br /> const short DEFAULT_ABR_MIN_MIN BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ;<br /> const unsigned short ABR_POLICY_MODERATE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ;<br /> <br /> atributo abrPolicy não assinado Atributo;<br /> não assinado em initialBitRate;<br /> atributo não assinado em minBitRate;<br /> atributo unsigned int maxBitRate;<br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br /> atributo double initialBufferTime;<br /> atributo double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> consente duplo DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> atributo double initialBufferTime;<br /> atributo double playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface TextFormat<br /> {<br /> // Color<br /> const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6 ;<br /> const unsigned short COLOR_BRIGHT_RED = 7 ;<br /> const unsigned short COLOR_DARK_GREEN = 8 ; <br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ; <br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;<br /> const unsigned short COLOR_BRIGHT _YELLOW = 16 ;<br /> const short COLOR_DARK_MAGENTA não assinado = 17 ;<br /> const short COLOR_MAGENTA não assinado = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ;<br /> const unsigned short COLOR_DARK_CYAN = 20 ;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ;<br /> <br /> atributo readonly short fontColor;&lt;a2 Atributo somente leitura não assinado short backgroundColor;<br /> atributo somente leitura unsigned short fillColor;<br /> atributo somente leitura unsigned short edgeColor;<br /> <br /> // Tamanho<br /> const short SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /> <br /> atributo readonly de tamanho curto não assinado;<br /> <br />/ FontEdge<br /> const short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_RAISED = 2 ;<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> atributo somente leitura não assinado fonte curta;<br /> <br /> // Fonte<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;&lt;a5 const short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CASUAL = 4 ;<br /> const short FONT_CURSIVE não assinado = 5 ;<br /> const short FONT_SMALL_CAPITALS não assinado = 6 ;<br /> atributo somente leitura fonte curta não assinada;<br /> atributo somente leitura unsigned short fontOpacity;<br /> atributo somente leitura unsigned short backgroundOpacity;<br /> atributo somente leitura Opacity;<br /> atributo somente leitura não assinado DEFAULT_OPACITY;<br /> };<br /><br /></p> </td> 
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
   <td><p>interface MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource resource, long resourceId,<br /> ItemLoaderListener listener, <br /> MediaPlayerItemConfig config) ;<br /> void cancel();<br /> atributo somente leitura MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>Novo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallback Func;<br /> }</p> </td> 
   <td>Novo para 2.0</td> 
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
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerItem {<br /> atributo somente leitura recurso MediaResource;<br /> atributo somente leitura longa resourceId;<br /> atributo somente leitura booleano live;<br /> <br /> atributo somente leitura booleano hasAlternateAudio;<br /> atributo somente leitura AudioTrackList audioTracks;<br /> atributo somente leitura Track seletedAudioTrack;<br /> void selectAudioTrack(AudioTrack track); <br /> <br /> atributo somente leitura booleano hasClosedCaptions;<br /> atributo somente leitura ClosedCaptionsTrackList closedCaptionsTracks;<br /> atributo somente leitura ClosedCaptionsTrack seletedCaptionsTrack;<br /> void selectClosedCaptionsTrack( a13/&gt; ClosedCaptionsTrack track); <br /> <br /> atributo somente leitura booleano hasTimedMetadata;<br /> atributo somente leitura TimedMetadataList timedMetadata;<br /> atributo somente leitura booleano dinâmico;<br /> <br /> atributo somente leitura booleano isProtected; a20/&gt; atributo somente leitura Perfis Perfil de Perfil somente leitura DRMMetadataInfoList drmMetadataInfos;<br /> atributo somente leitura Perfil selecionadoPerfil;<br /> <br /> atributo somente leitura booleano trickPlaySupported;<br /> atributo somente leitura FloatArray availablePlaybackRates;<br /> atributo somente leitura float seletedPlaybackRate;<br /> <br /> <br /> atributo somente leitura MediaPlayer mediaPlayer;<br /> atributo somente leitura MediaPlayerItemConfig configuração;&lt;a3 };<br /><br /><br /><br /></p> </td> 
   <td><p>interface MediaPlayerItem {<br /> atributo somente leitura recurso MediaResource;<br /> atributo somente leitura longa resourceId;<br /> atributo somente leitura booleano live;<br /> <br /> atributo somente leitura booleano hasAlternateAudio;<br /> atributo somente leitura AudioTrackList audioTracks;<br /> atributo AudioTrack seletedAudioTrack;<br /> <br /> <br /> atributo somente leitura booleano hasClosedCaptions;<br /> atributo somente leitura ClosedCaptionsTrackList ccTracks;<br /> atributo ClosedCaptionsTrack seletedCCTtrack;<br /> <br /> <br /> <br /> atributo somente leitura booleano hasTimedMetadata;<br /> atributo somente leitura TimedMetadataList timedMetadata;<br /> atributo somente leitura booleano dinâmico;<br /> <br /> atributo somente leitura booleano isProtected; <br /> atributo somente leitura DRMMetadataInfoList drmMetadataInfos;<br /> atributo somente leitura Perfis ProfileList;<br /> <br /> <br /> atributo somente leitura booleano trickPlaySupported;<br /> atributo somente leitura Int 32Array availablePlaybackRates;<br /> <br /> atributo somente leitura StringList adTags;<br /> <br /> atributo somente leitura MediaPlayer mediaPlayer;<br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> nome do atributo somente leitura DomString;<br /> atributo somente leitura DomString language;<br /> atributo somente leitura padrão booleano;<br /> atributo somente leitura booleano autoSelect;<br /> }; </p> </td> 
   <td>Novo para 2.0</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack : Track<br /> {<br /> nome do atributo somente leitura DomString; //FromTrack<br /> atributo somente leitura DomString language;//FromTrack<br /> atributo somente leitura padrão booleano; // De Track<br /> atributo somente leitura booleano autoSelect;//FromTrack<br /> <br /> atributo somente leitura int pid não assinado;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {<br /> atributo somente leitura Nome DomString;<br /> atributo somente leitura Linguagem DomString; <br /> atributo somente leitura padrão booleano;<br /> atributo somente leitura booleano autoSelect;<br /> atributo somente leitura booleano forçado;<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface AudioTrackList<br /> {<br /> atributo somente leitura de comprimento longo não assinado;<br /> getter AudioTrack (índice longo não assinado);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack : Track<br /> {<br /> nome do atributo somente leitura DomString; //FromTrack<br /> atributo somente leitura DomString language;//FromTrack<br /> atributo somente leitura padrão booleano; // FromTrack<br /> atributo somente leitura booleano autoSelect;//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const short SERVICE_WEB_VEB TT_CAPTIONS = 2;<br /> atributo somente leitura unsigned short serviceType;<br /> atributo somente leitura booleano forçado;<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> atributo somente leitura nome DomString;<br /> atributo somente leitura linguagem DomString;<br /> atributo somente leitura padrão booleano;<br /> <br /> <br /> atributo somente leitura booleano ativo;<br /> <br /> <br /> &lt;a10/ &gt; <br /> <br /> };<br /></p> </td> 
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
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Perfil: Nenhuma alteração para 2.0</td> 
   <td><p>interface Perfil<br /> {<br /> atributo somente leitura não assinado int width;<br /> atributo somente leitura não assinado int height;<br /> atributo somente leitura não assinado int bit Rate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>Lista de perfis: Nenhuma alteração para 2.0</td> 
   <td><p>interface ProfileList<br /> {<br /> atributo só de leitura comprimento longo não assinado;<br /> getter Profile(índice longo não assinado);<br /> };</p> </td> 
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
   <td><strong>DRMMetadataInfo</strong>: Nenhuma alteração para 2.0</td> 
   <td><p>interface DRMMetadataInfo<br /> { <br /> atributo somente leitura metadados DRMMetadata;<br /> atributo somente leitura longa prefetchTimestamp;<br /> atributo somente leitura TimeRange TimeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>: Nenhuma alteração para 2.0</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> atributo somente leitura de comprimento longo não assinado;<br /> getter DRMMetadataInfo(índice longo não assinado);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Mapeamento de erros do C++ para exceções em diferentes idiomas {#mapping-c-errors-to-exceptions-in-different-languages}

Você pode mapear códigos de erro C++ para exceções em diferentes idiomas.

O PSDK C++ tem uma política de &quot;sem lançamento&quot; para suas APIs. A maioria dos métodos de API retorna um valor PSDKErrorCode para indicar se o método foi executado com êxito. Erros assíncronos são notificados por meio dos eventos de erro.

O ActionScript e o JAVA PSDK têm uma política diferente. A maioria dos erros lançará um ArgumentError ou IllegalStateException para indicar que a parte síncrona do método não pôde ser executada. Essas exceções não são capturadas e o código do aplicativo é responsável por manipular as exceções. Normalmente, eles transmitem informações úteis sobre por que a chamada do método falhou. Por exemplo, se o comando prepareToPlay for chamado em um estado inválido, a seguinte exceção será lançada:

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

O ActionScript/JAVA também lança exceções de construtores para indicar que algum objeto interno foi criado incorretamente. Essas exceções são tratadas internamente e não são propagadas para o aplicativo. As exceções serão incluídas em uma notificação de aviso que é enviada ao aplicativo

Por exemplo, se nenhum arquivo de mídia válido foi encontrado para a resposta de anúncio recebida, nenhum objeto de ativo de anúncio ou anúncio válido poderá ser criado. Como resultado, nenhum anúncio é colocado na linha do tempo e uma notificação NotificationEvent.OperationFailed é enviada.

Os códigos de erro ou aviso que são recebidos de forma assíncrona do Adobe Video Engine (AVE) são enviados para o aplicativo como eventos normais. O evento de notificação contém todos os códigos de erro recebidos e quaisquer metadados adicionais, como URL, identificador de recurso, identificador de recurso, identificador e assim por diante. Se o erro for grave e a reprodução da mídia atual não puder continuar, o MediaPlayer será transferido para o status ERROR e o retorno de chamada onStatusChanged ou o evento MediaPlayerStatusChanged.STATUS_CHANGED será enviado. Se a reprodução continuar, um evento de notificação normal será enviado.

<table> 
 <tbody> 
  <tr> 
   <th>Erro C++ (Código PSDKError)</th> 
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
   <td>Exceção com código = 1, descrição = "INVALID_ARGUMENT" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>Exceção com código = 2, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>Exceção com código = 3, descrição = "ILLEGAL_STATE" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 4, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 5, descrição = "CREATION_FAILED" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 5, descrição = "CREATION_FAILED" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kCEAataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 7, descrição = "DATA_NOT_AVAILABLE" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 8, descrição = "SEEK_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 9, descrição = "UNSUPPORTED_FEATURE" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 10, descrição = "RANGE_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 11, descrição = "CODEC_NOT_SUPPORTED" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 12, descrição = "MEDIA_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 13, descrição = "NETWORK_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error ou MediaPlayerNotification.Warning</td> 
   <td>MediaError ou NotificationEvent</td> 
   <td>Exceção com código = 14, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 15, descrição = "INVALID_SEEK_TIME" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 16, descrição = "AUDIO_TRACK_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 17, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 18, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 19, descrição = "GENERIC_ERROR" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>Exceção com código = 200, descrição = "PLAYBACK_OPERATION_FAILED" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>Exceção com código = 201, descrição = "NATIVE_WARNING" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>Exceção com código = 202, descrição = "AD_RESOLVER_FAILED" e additionalInfo= &lt;conforme passado pelo método que emitiu esta exceção&gt;</td> 
  </tr> 
 </tbody> 
</table>

## Alterações no elemento da API do utilitário e da ajuda para 2.0 {#utility-and-helper-api-element-changes-for}

Essas tabelas comparam os elementos Utility e Helper API do JavaScript TVSDK entre as versões 1.3 e 2.0.

Tabelas neste tópico:

* Versão
* TimeRange
* QOSProvider
* DeviceInformation
* LoadInfo
* Exibir
* ReproduçãoInformações

### Versão {#version}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface Version<br /> {<br /> atributo somente leitura versão DomString;<br /> atributo somente leitura descrição DomString;<br /> atributo somente leitura major;<br /> atributo somente leitura menor;<br /> atributo somente leitura revisão longa;<br /> atributo somente leitura apiVersion longa;<br /> };</p> </td> 
   <td><p>interface Version<br /> {<br /> atributo somente leitura versão DomString;<br /> atributo somente leitura Descrição DomString;<br /> atributo somente leitura DomString major;<br /> atributo somente leitura DomString minor;<br /> atributo somente leitura DomString revisão;<br /> atributo somente leitura apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td>Nenhuma alteração para 2.0</td> 
   <td><p>interface TimeRange<br /> {<br /> atributo somente leitura unsigned long begin;<br /> atributo somente leitura final unsigned;<br /> atributo somente leitura de longa duração unsigned;<br /> };</p> </td> 
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
   <td><p>interface QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer player);<br /> void detachMediaPlayer();<br /> <br /> readonly attribute DeviceInformation deviceInformation;<br /> atributo somente leitura PlaybackInformation playbackInformation;<br /> };</p> </td> 
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
   <td><p>interface DeviceInformation<br /> {<br /> atributo somente leitura DomString os;<br /> <br /> <br /> <br /> atributo somente leitura DomString id;<br /> atributo somente leitura int densidadeDPI;<br /> atributo somente leitura int heightPixels;<br /> atributo somente leitura int width9;/&gt; atributo somente leitura booleano searchToKeyFrame;<br /> };<br /></p> </td> 
   <td><p>interface DeviceInformation<br /> {<br /> atributo somente leitura DomString os;<br /> atributo somente leitura int sdk;<br /> atributo somente leitura modelo DomString;<br /> atributo somente leitura fabricante DomString;<br /> atributo somente leitura DomString id;<br /> atributo somente leitura int DPI;<br /> somente leitura atributo int heightPixels;<br /> atributo somente leitura int widthPixels;<br /> <br /> };</p> </td> 
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
   <td><p>interface LoadInfo<br /> {<br /> atributo somente leitura url DomString;<br /> atributo somente leitura no tamanho;<br /> atributo somente leitura duplo download Duration;<br /> atributo somente leitura int periodIndex;<br /> atributo somente leitura double mediaDuration;<br /> atributo somente leitura curto TRACK_TYPE_FRAGMENT;<br /> Atribua somente atributo curto TRACK_TYPE_TRACK;<br /> somente leitura atributo curto TRACK_TYPE_MANIFEST;<br /> atributo somente leitura tipo curto;<br /> atributo somente leitura DomString trackName;<br /> atributo somente leitura DomString trackType;<br /> atributo somente leitura em trackIndex; 13/&gt; };<br /></p> </td> 
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
   <td><p>interface View<br /> {<br /> atributo somente leitura não assinado curto x;<br /> atributo somente leitura não assinado curto y;<br /> atributo somente leitura de largura curta não assinada;<br /> atributo somente leitura de altura curta não assinada;<br /> <br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### Informações da reprodução {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>APIs 2.0</th> 
   <th>APIs 1.3</th> 
  </tr> 
  <tr> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo somente leitura duplo timeToFirstByte;<br /> atributo somente leitura duplo timeToLoad;<br /> atributo somente leitura duplo timeToStart;<br /> atributo somente leitura duplo timeToFail;<br /> atributo somente leitura totalSecondsPlayed;<br /> somente leitura atributo int totalSecondsSpent;<br /> atributo somente leitura frameRate;<br /> atributo somente leitura int droppedFrameCount;<br /> atributo somente leitura intBandwidth;<br /> atributo somente leitura bitrate;<br /> atributo somente leitura bufferTime;<br /> atributo somente leitura intBuffer Comprimento;<br /> atributo somente leitura em emptyBufferCount;<br /> atributo somente leitura bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {<br /> atributo somente leitura duplo timeToFirstByte;<br /> atributo somente leitura duplo timeToLoad;<br /> atributo somente leitura duplo timeToStart;<br /> atributo somente leitura duplo timeToFail;<br /> atributo somente leitura totalSecondsPlayed;<br /> somente leitura atributo int totalSecondsSpent;<br /> atributo somente leitura double frameRate;<br /> atributo somente leitura int droppedFrameCount;<br /> <br /> atributo somente leitura int bitrate;<br /> atributo somente leitura bufferTime;<br /> atributo somente leitura int bufferLength;<br /> atributo readonly em emptyBufferCount;<br /> atributo somente leitura bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa na página [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) .
