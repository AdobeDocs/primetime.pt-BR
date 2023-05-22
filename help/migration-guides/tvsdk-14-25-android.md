---
title: TVSDK 1.4 para 2.5 para Android (Java)
description: O TVSDK 2.5 oferece vários benefícios em relação à versão 1.4 em termos de desempenho, segurança, melhores integrações e muito mais.
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
exl-id: 3b7f8355-ebea-4322-aef4-5393308391b5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '2323'
ht-degree: 0%

---

# TVSDK 1.4 para 2.5 para Android (Java) {#tvsdk-to-for-android-java}

O TVSDK 2.5 oferece vários benefícios em relação à versão 1.4 em termos de desempenho, segurança, melhores integrações e muito mais.

O TVSDK resolve os maiores desafios no dispositivo que é mais importante. O Android continua seu domínio global, com mais de 86% de participação no mercado. A migração para o TVSDK no Android otimizará o desempenho da reprodução para melhorar o envolvimento do usuário e acelerar o tempo de entrada no mercado com suporte para novos formatos de conteúdo.

## Benefícios da migração para o TVSDK v2.5 {#benefits-of-migrating-to-tvsdk-v}

O TVSDK 2.5 oferece vários benefícios em relação à versão 1.4 em termos de desempenho, segurança, melhores integrações e muito mais. Leia para conhecer rapidamente os benefícios da migração para essa nova versão.

De acordo com um estudo de benchmark de terceiros, a v2.5 fornece uma redução de 5x no tempo de inicialização e de 3,8x nos quadros ignorados, em relação à média do setor.

| Recursos de desempenho | Descrição |
|--- |--- |
| Ativação instantânea para VOD e Live | Pré-carregar os segmentos ts iniciais para Reprodução imediata para VOD e fluxos lineares ao vivo ao alternar canais, para uma experiência semelhante à da TV. |
| Carregamento de anúncio lento | Inicia a reprodução assim que o conteúdo ou antes da exibição está disponível ao resolver anúncios intermediários em um thread paralelo. |
| Conexões de rede persistentes | Aumento da eficiência e diminuição da latência do código de rede para obter um desempenho de reprodução mais rápido. |
| Lógica ABR aprimorada | A nova lógica ABR é baseada no comprimento do buffer, na taxa de alteração do comprimento do buffer e na largura de banda medida. Isso garante que o ABR escolha a taxa de bits certa quando a largura de banda flutuar e também otimize o número de vezes que o switch de taxa de bits realmente ocorre, monitorando a taxa em que o comprimento do buffer muda. |
| Download de segmento parcial | Inicia a reprodução assim que quadros suficientes de um segmento estão disponíveis para renderizar o vídeo de forma confiável no lado do cliente. |
| Downloads paralelos | O TVSDK baixa segmentos de áudio e vídeo em paralelo para conteúdo desmesclado para otimizar o desempenho da reprodução. |

Os recursos de reprodução melhoram o engajamento do consumidor, fornecendo a experiência de transmissão linear em digital. Além disso, ajuda a aproveitar o DRM nativo, como o Widevine para reprodução de alta definição.

| Recursos de reprodução | Descrição |
|--- |--- |
| Reprodução de MP4 | Os clipes MP4 curtos não precisam ser retranscodificados para reprodução no TVSDK. |
| Reprodução de conteúdo de VOD do TRAÇO | Há suporte para casos de uso básicos de reprodução de VOD DASH. |
| Truque suave com o ABR | Suporte para avanço rápido e retrocesso no HLS usando quadros-chave em taxas baixas e I-Frames em velocidades mais rápidas. Suporte a ABR para todos os quadros suportados. |

Os recursos são importantes para atender às restrições do estúdio, como reprodução de alta definição sobre DRM nativo.

| Recursos | Descrição |
|--- |--- |
| Proteção de saída com base em resolução | a reprodução pode ser restrita a apenas determinadas resoluções permitidas pelos requisitos de DRM. Disponível somente por meio do Primetime DRM. |
| Suporte Widevine | Compatível com fluxos de VOD DASH para ativar casos de uso de DRM nativo. |

O aprimoramento do faturamento direto dispensa a necessidade de criar relatórios manuais para faturamento todos os meses. O VHL 2.0 permite um tempo de comercialização mais rápido com integração de pré-compilação e melhor precisão no rastreamento.

| Recursos | Descrição |
|--- |--- |
| Integração do Mat | Suporte para medição de visibilidade de anúncio do Mat. |
| VHL 2.0 | A mais recente integração otimizada da biblioteca de heartbeats de vídeo para a coleta automática de dados de uso do Adobe Analytics. |
| Suporte a failover | Estratégias adicionais implementadas para continuar a reprodução ininterrupta, apesar das falhas de servidores host, arquivos de lista de reprodução e segmentos. |
| Integração de faturamento direto | Envia métricas de cobrança para o back-end do Adobe Analytics, que é certificado pela Adobe Primetime para fluxos usados pelo cliente. |

>[!NOTE]
>
>Todos os recursos do TVSDK v1.4 são compatíveis com a v2.5, exceto o suporte a vários CDNs.

## Visão geral do processo de migração {#overview-of-the-migration-process}

A migração sem problemas do TVSDK 1.4 para o 2.5 envolve a alteração para as bibliotecas da versão 2.5, recompilação e o uso deste documento para ajudar a depurar quaisquer problemas que ocorram.

As bibliotecas TVSDK v1.4 não funcionam com as bibliotecas v2.5 e coexistem com elas. Você deve usar as bibliotecas v2.5 com TVSDK 2.5 e migrar seus aplicativos e integrações para atualizar para o TVSDK 2.5. Este documento descreve como e o que alterar no código do aplicativo e como corrigir erros durante a recompilação.

O arquivo psdk.jar usa bibliotecas de terceiros para suportar diferentes recursos. Para evitar a remoção de bibliotecas, inclua o seguinte na `proguard.cfg` arquivo:

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

No `build.gradle` você precisa incluir a diretiva de compilação para incluir os arquivos JAR baseados em TVSDK. Se o aplicativo incluir o Adobe Video Analytics, será necessário incluir a diretiva de compilação para os jars adicionais necessários para a integração do Adobe Video Analytics no aplicativo

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

Várias alterações secundárias não são abordadas neste documento. Para conhecer as pequenas alterações na API, consulte [TVSDK 2.5 para API Java do Android](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html). A referência à API C++ correspondente tem descrições detalhadas. Para obter a documentação da API C++ análoga, consulte [TVSDK 2.5 para API C++ do Android](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html).

Vários exemplos de uso da API são abordados na implementação de referência distribuída com o TVSDK.

## Alterações na API no TVSDK v2.5 {#api-changes-in-tvsdk-v}

As APIs novas, obsoletas e modificadas estão documentadas abaixo.

| TVSDK v1.4 | TVSDK v2.5 | Descrição |
|--- |--- |--- |
| importar com.adobe.ave.drm .DRMAcquireLicenseSettings | importar com.adobe.mediacore.drm .DRMAcquireLicenseSettings; | Todos os nomes de classe na API TVSDK 2.5 começam com o prefixo com.adobe.mediacore. Este é apenas um exemplo. |
| MediaPlayerException, IllegalStateException ou IllegalArgumentException | MediaPlayerException | Na versão 2.5, as APIs geram apenas MediaPlayerException. |
| MediaPlayer.PlayerState (MediaPlayer.Event.PLAYBACK) | MediaPlayerStatus (MediaPlayerEvent.STATUS_CHANGED) | Na v2.5, MediaPlayer.PlayerState foi renomeado para uma enumeração separada de MediaPlayerStatus. |
| DefaultMediaPlayer.create (getActivity().getApplicationContext()) | MediaPlayer mediaPlayer = novo MediaPlayer(getActivity(). getApplicationContext()); | Os métodos estáticos usados para criar objetos são substituídos por construtores públicos. |
| MediaPlayer.seekToLocalTime() | MediaPlayer.seekToLocal() | O método MediaPlayer.seekToLocalTime() agora é chamado de MediaPlayer.seekToLocal(). |
| closedCaptionsTrack.isActive() |  | Não disponível |
| MetadataNode | Metadados | Na v2.5, a classe Metadata substitui o uso da classe MetadataNode v1.4. |
| DefaultMetadataKeys | TeclasDeMetadados | O DefaultMetadataKeys da v1.4 está em MetadataKeys de enumeração v2.5. |
| AdvertisingFactory | ContentFactory | A AdvertisingFactory da v1.4 foi renomeada para ContentFactory na v2.5 |
| DetectorOportunidadePosicionamento | OpportunityGenerator | Os detectores são substituídos por Geradores. |
| mediaPlayer.getView().notifyClick(); | mediaPlayer.notifyClick(); | O método notifyClick() de MediaPlayerView foi movido para a classe MediaPlayer. |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, int nMaxBitRate) | public ABRControlParameters(int nInitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate, int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate) |  |
| playbackInformation.getTimeToFirstFrame() |  | Não disponível |
|  | playbackInformation.get PerceivedBandwidth() | O TVSDK v2.5 QOSProvider tem uma nova propriedade para determinar a largura de banda percebida durante uma sessão de transmissão. |

### Classes removidas {#removed-classes}

As classes a seguir são removidas e não têm equivalentes.

* `TimeRangeCollection`
* `PSDKConfig`
* `BaseLogger`
* `DefaultLogger`
* `Log`
* `Logger`
* `LogFactory`
* `NullLogger`

As seis últimas classes estão disponíveis como classes de utilitários na implementação de referência.

## Alterações de namespace {#namespace-changes}

A API TVSDK 2.5 consolida namespaces.

Todos os nomes de classe na API TVSDK 2.5 começam com o prefixo com.adobe.mediacore. Alguns nomes de classe na API TVSDK 1.4 começam com com com.adobe.ave. As classes 2.5 correspondentes alteram com.adobe.ave para com.adobe.mediacore. Por exemplo, observe as alterações nas seguintes linhas de código para 1.4 e 2.5:

```java
// TVSDK 1.4
import com.adobe.ave.drm.DRMAcquireLicenseSettings; import com.adobe.ave.drm.DRMLicense;
import com.adobe.ave.drm.DRMManager; import com.adobe.ave.drm.DRMMetadata
```

```java
// TVSDK 2.5
import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; import com.adobe.mediacore.drm.DRMLicense;
import com.adobe.mediacore.drm.DRMManager; import com.adobe.mediacore.drm.DRMMetadata;
```

## Alterações na manipulação de eventos {#changes-in-event-handling}

Para registrar eventos nesta versão, passe o manipulador para `addEventListener`. A lista de eventos foi substancialmente revista da versão 1.4 para a versão 2.5.\
Por exemplo, veja como registrar um manipulador de eventos para `MediaPlayerEvent.STATUS_CHANGED:`

```java
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,
new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
});
```

O evento foi registrado da seguinte forma na versão 1.4:

```java
mPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {
@Override
public void onStateChanged(MediaPlayer.PlayerState state,
MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});
```

A enumeração MediaPlayerEvent contém todos os códigos de evento. Os seguintes códigos de evento da versão 1.4 não existem mais na versão 2.5:

* `ADBREAK_PLACEMENT_COMPLETED`
* `ADBREAK_PLACEMENT_FAILED`
* `ADBREAK_REMOVAL_COMPLETED`
* `AD_BREAK_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_FAILED`
* `AUDIO_TRACK_FAILED`
* `BACKGROUND_MANIFEST_FAILED`
* `BUFFERING_FULL, CUSTOM_AD_EVENT`
* `CONTENT_MARKER`
* `CONTENT_PLACEMENT_COMPLETE`
* `CONTENT_CHANGED`
* `ITEM_REPLACED`
* `ITEM_READY`
* `VIEW_CLICKED`
* `PREPARED`
* `UPDATED`
* `OPPORTUNITY_COMPLETED`
* `OPPORTUNITY_CREATED`
* `OPPORTUNITY_FAILED`
* `PAUSE_AT_PERIOD_END`
* `PLAYBACK_STARTED`
* `PLAYBACK_PAUSED`
* `PLAYBACK_COMPLETED`
* `PLAY_COMPLETE`
* `POST_ROLL_COMPLETE`
* `RESOURCE_LOADED`
* `TIMED_METADATA_SKIPPED`
* `VIDEO_ERROR`
* `VIDEO_STATE_CHANGED`

Os seguintes códigos de evento são novos na versão 2.5:

* `AD_RESOLUTION_COMPLETE`
* `BUFFER_PREPARED`
* `CAPTIONS_UPDATED`
* `MANIFEST_UPDATED`
* `PLAYBACK_RANGE_UPDATED`
* `RESERVATION_REACHED`
* `TIME_CHANGED`
* `TIMED_EVENT`
* `TIMED_METADATA_ADDED_IN_BACKGROUND`

### Eventos renomeados {#renamed-events}

| Novo nome | Nome antigo |
|--- |--- |
| SEEK_BEGIN | SEEK_STARTED |
| SEEK_END | BUSCA_CONCLUÍDA |
| SEEK_POSITION_ADJUSTED | SEEK_ADJUST_COMPLETED |
| BUFFERING_BEGIN | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATUS_CHANGED | STATE_CHANGED |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_ADDED |
| TAMANHO_DISPONÍVEL | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## Alterações no MediaPlayer {#mediaplayer-changes}

Uma nova forma de construir `MediaPlayer` e alterações em alguns dos métodos.

**Alterações na classe MediaPlayer**

Estas são as alterações de `MediaPlayer` classe:

* A variável `MediaPlayerStatus` enum substitui `MediaPlayer.PlayerState`. Por exemplo:

```java
//TVSDK v1.4
mPlayer. addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {

@Override
public void onStateChanged(MediaPlayer.PlayerState state,MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});

//TVSDK v2.5
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
//Additional handlers.
...
});
```

* A variável `MediaPlayer.seekToLocalTime()` agora, o método é chamado de `MediaPlayer.seekToLocal`. Por exemplo:

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* A variável `MediaPlayerView.notifyClick()` o método agora é `MediaPlayer.notifyClick()`. Por exemplo:

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* A primeira `MediaPlayer.MediaPlayer.getNotificationHistory()` agora o método foi removido e não foi substituído.
* A primeira `MediaPlayer.replaceCurrentItem()` O é dividido em dois métodos: `replaceCurrentResource()`, que utiliza uma instância de `MediaResource`, e `replaceCurrentItem()`, que utiliza uma instância de `MediaPlayerItem`. Por exemplo:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());

mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5 - replacing a resource
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());
...
try {
mMediaPlayer.replaceCurrentResource(playerResource, _mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
// TVSDK 2.5 - replacing an Item
MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(context, new MediaPlayerItemLoader.LoaderListener() {

@Override
public void onError(PSDKErrorCode psdkErrorCode, String s) {
...
}
@Override
public void onLoadComplete(MediaPlayerItem mediaPlayerItem) {
...
}
@Override
public void onBufferingBegin() {
...
}
@Override
public void onBufferPrepared() {
...
}
});
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());

itemLoader.load(playerResource); itemLoader.prepareBuffer();
mediaPlayer.replaceCurrentItem(itemLoader.getItem());
```

Você pode usar essa opção para alternar entre instâncias pré-inicializadas do MediaPlayer, como no caso de blecautes.

**Construtores substituem métodos create() estáticos**

Você pode usar construtores no TVSDK v2.5, em vez de usar `create()` métodos do TVSDK v1.4. Todas as classes com nomes que começam com Padrão, como `DefaultMediaPlayer`, `DefaultNetworkConfig`, `DefaultContentFactory`, não estão disponíveis na v2.5.

Em alguns casos, a API TVSDK v1.4 usa o seguinte padrão para criar classes:

1. Definir uma interface (por exemplo, `MediaPlayer`).
1. Forneça uma classe padrão (por exemplo, `DefaultMediaPlayer`).
1. Forneça um `create()` na classe padrão para fornecer uma classe que implementa a interface.

No TVSDK v2.5, essas interfaces são classes concretas e você cria instâncias dessas classes usando os respectivos construtores. Os trechos de código a seguir ilustram essa diferença:

```java
//TVSDK v1.4
// Create a media player
// MediaPlayer is an interface
private MediaPlayer createMediaPlayer() { MediaPlayer mediaPlayer =
DefaultMediaPlayer.create(getActivity().getApplicationContext()); return mediaPlayer;

//TVSDK v2.5
// Create a media player
// MediaPlayer is a class that you instantiate private MediaPlayer createMediaPlayer() {
MediaPlayer mediaPlayer =
new MediaPlayer(getActivity().getApplicationContext()); return mediaPlayer;
}
```

Outras classes que não seguem esse padrão, mas usam `create()` Os métodos descritos no ponto 1.4 incluem:

* MediaResource\
   Isso era usado anteriormente `MediaResource.createFromUrl()`. Agora use o construtor, que usa um URL, tipo de recurso e metadados. Por exemplo:

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());
mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, getAdvertisingMetadata());

try { mediaPlayer.replaceCurrentResource(playerResource,_mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
```

* Anúncio
* AdAsset
* AdBreak

Algumas classes (por exemplo `ContentFactory`) são classes abstratas sem implementação padrão disponível publicamente (por exemplo, `DefaultContentFactory`). Nesses casos, você pode fornecer uma implementação padrão por meio de uma função de conveniência, por exemplo: `mediaPlayerItemConfig.getDefaultContentFactory()`

**Alterações nas legendas ocultas**

As seguintes alterações afetam as classes relacionadas às legendas ocultas:

* Ao recuperar faixas de legendas ocultas, `MediaPlayerItem.getClosedCaptionTracks()` retorna somente as faixas ativas.
* `ClosedCaptionTrack` não tem mais um `isActive()` método.

```java
//TVSDK v1.4
public List<String> getClosedCaptionTracks(String label) {
List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks(); Iterator<ClosedCaptionsTrack> iterator =
closedCaptionsTracks.iterator();
if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); String isActive = closedCaptionsTrack.isActive() ? " (" + label
+ ")" : "";
closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName()
+ " : " + closedCaptionsTrack.getLanguage() + isActive);
}
}
return closedCaptionsTracksAsStrings;
}

//TVSDK v2.5
public List<String> getClosedCaptionTracks(String label) {

MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks();
Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator();

List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); closedCaptionsTracksAsStrings.
add(closedCaptionsTrack.getName() + " : ");
}
}
return closedCaptionsTracksAsStrings;
}
// Add snippet and desc for CaptionsUpdatedEventListener mediaPlayer.addEventListener(MediaPlayerEvent.CAPTIONS_UPDATED,
captionsUpdatedEventListener);

private final CaptionsUpdatedEventListener captionsUpdatedEventListener = new CaptionsUpdatedEventListener() {

@Override
public void onCaptionsUpdated(MediaPlayerItemEvent mediaPlayerItemEvent) { getActivity().findViewById(R.id.sbPlayerControlCC).setVisibility(
View.VISIBLE/*Visible*/);
}
};
```

## Alterações de publicidade {#advertising-changes}

Há várias alterações relacionadas a anúncios na versão 2.5.

**Alterações no comportamento de publicidade**

O comportamento padrão da reprodução de anúncio quando um usuário executa uma busca além de um pod de anúncio é ligeiramente alterado na v2.5. Se o ad break não for assistido, o anúncio será reproduzido depois de uma busca. Quando o aplicativo está usando a política de anúncios padrão, o ad break é removido após a conclusão da reprodução. Usando o TVSDK v2.5, se um usuário buscar por trás de um pod de anúncio na linha do tempo e o ad break não for assistido, nenhum anúncio será reproduzido.

No entanto, no TVSDK v1.4, por padrão, um anúncio é reproduzido no caso de uma busca retroativa. Por exemplo, se você buscar de trás para frente entre o terceiro e o quarto ad break, o comportamento padrão do TVSDK v1.4 é reproduzir o terceiro ad break.

**Alteração nas regras de publicidade**

As Regras de publicidade são especificadas usando um arquivo JSON. O formato do arquivo JSON permanece o mesmo nas duas versões do TVSDK. No entanto, no TVSDK v2.5, o arquivo JSON de regras de anúncios deve ser hospedado em um local acessível por meio de um URL HTTP. O aplicativo pode usar uma instância do AuditudeSettings.

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

No TVSDK versão 1.4, esse arquivo é colocado abaixo da pasta de ativos no aplicativo e o TVSDK carrega o arquivo.

**Renomeação de fábrica de anúncios**

`AdvertisingFactory` agora se chama `ContentFactory`. Com `ContentFactory` você pode criar workflows de publicidade personalizados substituindo alguns de seus métodos. Use return null para manter os comportamentos padrão, como no seguinte:

```java
//TVSDK v2.5
new ContentFactory() {
@Override
public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item) { return new CustomAdPolicySelector();
}
@Override
public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { return null;
}
@Override
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { return null;
}
@Override
public List<CustomAdHandler> retrieveCustomAdPlaybackHandlers(MediaPlayerItem item) { return null;
}
};
```

**Quebras de anúncio de comprimento zero**

O TVSDK 2.5 insere ad breaks de comprimento zero como espaços reservados quando o servidor de publicidade não retorna nenhum anúncio.

Os ad breaks de comprimento zero podem ser determinados detectando a contagem de anúncios como zero no ad break usando o evento onAdBreakStarted, e o aplicativo deve lidar com esses ad breaks adequadamente.

**Alterações de metadados**

A classe Metadata fornece uma substituição mais eficiente para a antiga classe MetadataNode.

* A classe Metadata pode armazenar strings, matrizes de bytes e outros objetos Metadata:

```java
TVSDK v1.4
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new MetadataNode();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingParameters(advertisingParams);

return adSettings;
}
//TVSDK v2.5
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new Metadata();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingInfo(advertisingParams);

return adSettings;
}
```

* A variável `MetadataKeys` enum substitui `DefaultMetadataKeys`. Nem todas as chaves em `DefaultMetadataKeys` estão presentes na nova versão.

```java
//TVSDK v1.4
if (this.mediaPlayer != null && this.mediaPlayer.getCurrentItem() != null) { MetadataNode resourceMetadata =
(MetadataNode) this.mediaPlayer.getCurrentItem().getResource().getMetadata();
VideoAnalyticsMetadata vaMetadata = (VideoAnalyticsMetadata)
resourceMetadata.getNode(DefaultMetadataKeys.
VIDEO_ANALYTICS_METADATA_KEY.getValue());
}

//TVSDK v2.5
if (resourceMetadata.containsKey(VideoAnalyticsMetadata.
VIDEO_ANALYTICS_METADATA_KEY)) {
JSONObject vaMetadataObj =
new JSONObject(resourceMetadata.
getValue(VideoAnalyticsMetadata. VIDEO_ANALYTICS_METADATA_KEY));
vaMetadata = parseVideoAnalyticsMetadata(vaMetadataObj);
}

} catch (JSONException e) { e.printStackTrace();
}
```

* Os metadados publicitários são agora `AdvertisingMetadata` classe, uma subclasse de Metadados, e agora é armazenada em `MediaPlayerItemConfig` em vez de `MediaResource`.

```java
//TVSDK v1.4
MetadataNode mediaMetadata = new MetadataNode();

if (stream.live) { mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(),
getAdSettingsForLive());
} else {
mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(), getAdSettingsForVod());
}
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

if (stream.live) {
AuditudeSettings adSettings = getAdSettingsForLive(); adSettings.setLivePreroll(true); mediaItemConfig.setAdvertisingMetadata(adSettings);
} else {
// Set the advertising parameters for VOD. mediaItemConfig.setAdvertisingMetadata(getAuditudeSettingsForVod());
}

// Create advertising metadata node Metadata mediaMetadata = new Metadata();

// Asset Url
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, mediaMetadata);
try {
mediaPlayer.replaceCurrentResource(playerResource, mItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
//handle exception.
}
```

Metadados de configuração de rede, anteriormente membro do `MediaResource` classe, agora é representado pela classe `NetworkConfiguration` classe, e agora está armazenado em `MediaPlayerItemConfig` em vez de `MediaResource`.

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**Alterações na análise de TimedMetadata**

A análise de `TimedMetadata` foi alterado na versão 2.5 em relação aos tipos de dados para analisar a tag ID3.

```java
//TVSDK v1.4
public void onTimedMetadata(TimedMetadata timedMetadata) { TimedMetadata.Type type = timedMetadata.getType();
if (type.equals(TimedMetadata.Type.ID3)){ PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata(); Set<String> keys = metadata.keySet();
for (String key : keys) {
String value = metadata.getValue(key); PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"Key = " + key + " Value = " + value);
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { parseSCTE35Tag(timedMetadata);
}
}
}

//TVSDK v2.5
public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { PMPDemoApp.logger.i(LOG_TAG + " inside"," ontimedmetadata"); TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata();

TimedMetadata.Type type = timedMetadata.getType(); if (type.equals(TimedMetadata.Type.ID3)) {
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata();
if (metadata != null) { PMPDemoApp.logger.i(LOG_TAG +
"::expandID3Metadata", "isEmpty " + metadata.isEmpty());
Set<String> keys = metadata.keySet(); PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"No of keys=" + keys.size());
String s;
for (String key : keys) {
byte[] value = metadata.getByteArray(key); s = new String(value);
if (key.equalsIgnoreCase("APIC"))
s = "SUPPRESSING BINARY DATA FOR ATTACHED PICTURE.";
PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"Key=" + key + ", Length=" + value.length + ", Value=" + s.trim());
}
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { PMPDemoApp.logger.i(LOG_TAG +
" inside ontimedmetadata"," ext"); parseSCTE35Tag(timedMetadata);
}
}
}
```

**Outras alterações**

As seguintes alterações adicionais estão disponíveis na versão 2.5:

* A variável `notifyClick()` o método foi movido de `MediaPlayerView` para `MediaPlayer`.

* `AdPolicySelector` é uma interface, não uma classe. Implemente todos os seus métodos.
* `AdPolicyInfo` agora contém uma lista de `AdBreakTimelineItem`, não `AdBreakPlacement`.

* Nome da API de `ContentResolver` classe abstrata é alterada.
* `PlacementOpportunityDetector` O não está mais disponível. Em vez disso, estenda o `OpportunityGenerator` classe abstrata. A implementação de referência fornece um exemplo disso.

* Os parâmetros da variável `AdBreakPlacement` são iguais, mas em uma ordem diferente. Para obter uma implementação de exemplo, consulte a implementação do reprodutor de referência fornecida com o produto.

## Alterações no DRM {#changes-in-drm}

A maioria das alterações nessa versão está na camada DRM. A tabela a seguir mostra as alterações adicionais entre as versões 1.4 e 2.5:

| Método DRMManager | Retorno de chamada com sucesso no 1.4 | Retorno de chamada de erro em 1.4 | Ouvinte no 2.5 |
|--- |--- |--- |--- |
| acquisitionLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| acquisitionPreviewLicense | DRMLicenseAcquiredCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| autenticar | DRMAuthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | ND | DRMOperationErrorCallback | DRMErrorListener |
| inicializar | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leaveLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| resetDRM | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| returnLicense | DRMLicenseReturnCompleteCallback | DRMOperationErrorCallback | DRMReturnLicenseListener |
| setAuthenticationToken | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| storeLicenseBytes | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |

```java
//TVSDK 1.4
private final MediaPlayer.DRMEventListener _drmEventListener = new MediaPlayer.DRMEventListener() {

@Override
public void onDRMMetadata(final DRMMetadataInfo drmMetadataInfo) { PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata available
// event and the play event, so launch the metadata interface
// and give it the loaded metadata bytes, but only once
_drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo == null ||
!DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG + "#onDRMMetadata", "DRM auth is not needed."); return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold
// between the current player time and the DRM metadata start
// time. For the time being, we resolve it as soon as we receive
// the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG + "#onDRMMetadata", "DRMManager is null."); return;
}
SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity()); String authUser =
sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG + "#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(long majorCode,
long minorCode, Exception e) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + majorCode + " 0x" + Long.toHexString(minorCode));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};

//TVSDK 2.5
private final DRMMetadataInfoEventListener drmMetadataInfoEventListener = new DRMMetadataInfoEventListener() {
@Override
public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { final DRMMetadataInfo drmMetadataInfo =
drmMetadataInfoEvent.getDRMMetadataInfo();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata
// available event and the play event, so launch the
// metadata interface and give it the loaded metadata
// bytes, but only once
drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo ==
null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG +
"#onDRMMetadata",
"DRM auth is not needed.");
return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold between
// the current player time and the DRM metadata start time. For the
// time being, we resolve it as soon as we receive the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG +
"#onDRMMetadata", "DRMManager is null.");
return;
}

SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity());
String authUser = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(int major,
int minor,
String erroString, String serverErrorURL) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + major +
" 0x" +
Long.toHexString(minor));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};
```

O estático `DRMManager` instância que estava disponível na versão 1.4 após a criação de mediaplayer agora está disponível após a `onDRMMetadataInfo` ouvinte de eventos acionado.

## Alterações relacionadas à taxa de bits adaptável (ABR) {#adaptive-bitrate-abr-related-changes}

**Alterações nas constantes**

Muitas constantes alteraram o tipo de `String` para `int`. Por exemplo: `MediaResourceType`, `ABRControlParameters`, e `MediaPlayerStatusChangeEvent`.

```java
//TVSDK v1.4
ABRControlParameters
private void setAbrControlParams() { SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity());
if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED,
PMPDemoApp.DEFAULT_ABR_ENABLED)) {
int initialBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE, 0);
int minBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE, 0);
int maxBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE, PMPDemoApp.DEFAULT_MAX_BIT_RATE);
int mbrPolicyAsInt =
getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, 0); ABRControlParameters.ABRPolicy abrPolicy = policyFromInt(mbrPolicyAsInt); abrPolicy = abrPolicy != null ?
abrPolicy : ABRControlParameters.ABRPolicy.ABR_MODERATE;
_mediaPlayer.setABRControlParameters(new ABRControlParameters(initialBitRate,
minBitRate, maxBitRate, abrPolicy));
}
}

//TVSDK v2.5
ABRControlParameters
private void setAbrControlParams() { ABRControlParametersBuilder abrBuilder =
new ABRControlParametersBuilder();

if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED, PMPDemoApp.DEFAULT_ABR_ENABLED)) {

abrBuilder.setInitialBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE,
ABRControlParameters.DEFAULT_ABR_INITIAL_BITRATE)); abrBuilder.setMinBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxPlayoutRate(getDoublePreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_PLAYOUT_RATE,
ABRControlParameters.DEFAULT_MAX_PLAYOUT_RATE)); abrBuilder.setMinTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxTrickPlayBandwidthUsage(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BANDWIDTH,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE));

switch (getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, -1)) {
case 0: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_CONSERVATIVE); break;
case 1: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_MODERATE); break;
case 2: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_AGGRESSIVE); break;
default: abrBuilder.setPolicy(ABRControlParameters.DEFAULT_ABR_POLICY);
}
}
_mediaPlayer.setABRControlParameters(abrBuilder.toABRControlParameters());
}
```

**Alterações no construtor ABRControlParameters**

Alguns parâmetros foram adicionados, alguns renomeados e outros movidos. A seguir está a assinatura do construtor na v1.4 e a nova assinatura na 2.5:

```java
//TVSDK v1.4
public ABRControlParameters(ABRPolicy abrPolicy,
int nInitialBitRate, int nMinBitRate,
int nMaxBitRate)

//TVSDK v2.5
public ABRControlParameters(int nInitialBitRate,
int nMinBitRate, int nMaxBitRate,
ABRPolicy abrPolicy,
int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate,
int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate)
```

## Manipulação e eventos de erro {#error-events-and-handling}

**Alterações na manipulação de erros**

A variável `MediaError` A classe foi substituída pela classe `Notification` classe. A única diferença entre as classes `MediaError` e `Notification` é que o último não contém um atributo description. Os códigos de erro TVSDK 1.4 com valores 101xxx, 102xxx,104xxx,106xxx,107xxx,109xxx não existem no TVSDK 2.5. Para obter os códigos de reprodução no TVSDK 2.5, consulte [Erro nativo - valores de reprodução de vídeo](assets/psdk_android_2.5.pdf).

A seguir estão exemplos de tratamento de erros no TVSDK 1.4 e 2.5:

```java
//TVSDK v1.4
@Override
public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");

switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR: PMPDemoApp.logger.e(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: " + notification + "."); getActivity().finish();
break;
default:
// do nothing
}
}

//TVSDK v2.5
private final StatusChangeEventListener statusChangeEventListener = new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent mediaPlayerStatusChangeEvent)
{
MediaPlayerStatus state = mediaPlayerStatusChangeEvent.getStatus(); PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");
switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR:
PMPDemoApp.logger.e(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: ");
printErrorMetadata(mediaPlayerStatusChangeEvent.getMetadata()); showToast("MediaPlayer status ERROR: Look at the logs for details"); getActivity().finish();
break;
default:
// do nothing
}
}
};
```

Todos os erros recuperáveis são tratados como avisos e tratados usando o `NotificationEventListener` no TVSDK 2.5. Os avisos são exibidos como notificações com a `onOperationFailed` Ouvinte no manipulador de QOS no TVSDK 1.4, onde, como no TVSDK 2.5, a Notificação é um evento separado. O aviso tratado em 1.4 e 2.5 é o seguinte:

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener()
{
@Override
public void onBufferStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
}
@Override
public void onBufferComplete() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
}
@Override
public void onSeekStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
}
@Override
public void onSeekComplete(long adjustedTime) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
}
@Override
public void onLoadInfo(LoadInfo loadInfo) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize() + " bytes, media duration: " + loadInfo.getMediaDuration() + "ms, download duration: " + loadInfo.getDownloadDuration() + "ms");
}
@Override
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - ").append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append

//TVSDK v2.5
private final NotificationEventListener notificationEventListener = new NotificationEventListener() {
/**
* An example of dumping the information within a Notification. Here, we don't handle the event in
* any way except to print a log message.
* @param event The NotificationEvent
*/
@Override
public void onNotification(NotificationEvent event) { Notification notification = event.getNotification(); Notification.Type type = notification.getType(); StringBuilder sb = new StringBuilder(); sb.append("[").append(type).append("]");
sb.append(" Player operation failed (").append(notification.getCode()).append(")"); Metadata metadata = notification.getMetadata();
if (metadata != null)
{
for (String key : metadata.keySet())
{
sb.append(", ").append(key).append(" = ").append(metadata.getValue(key));
}
}
Notification inner = notification.getInnerNotification(); if (inner != null) {
sb.append(" :: Inner Notification [").append(inner.getType()).append("](").append(inner.getCode()).append(")");
Metadata innerMetadata = inner.getMetadata(); if (innerMetadata != null) {
for (String iKey : innerMetadata.keySet()) { sb.append(", ").append(iKey).append(" =
").append(innerMetadata.getValue(iKey));
}
}
}
switch(type)
{
case ERROR:
PMPDemoApp.logger.e(LOG_TAG, sb.toString()); break;
case WARNING:
PMPDemoApp.logger.w(LOG_TAG, sb.toString()); break;
default:
PMPDemoApp.logger.i(LOG_TAG, sb.toString()); break;
}
showToast(sb.toString()); PMPDemoApp.logger.d(LOG_TAG, sb.toString());
}
};
```

**Novas exceções**

Embora o TVSDK v1.4 tenha usado uma combinação de nulos, retornos de erro e uma variedade de exceções ( `MediaPlayerException`, `IllegalStateException`, e `IllegalArgumentException`), TVSDK v2.5 `generatesMediaPlayerException` para todos os erros.

>[!NOTE]
>
>Para obter detalhes sobre MediaPlayerException, é possível usar `getErrorCode()`.

Um exemplo da alteração está abaixo:

```java
//TVSDK v1.4
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (IllegalArgumentException e) { PrimetimeReference.logger.w(LOG_TAG +
"#setBufferControlParams",
"Unable to apply buffering params: " + e.getMessage() + ".");
}
}

//TVSDK v2.5
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (MediaPlayerException e) { PrimetimeReference.logger.w(LOG_TAG + "#setBufferControlParams", "Unable to apply buffering params: " + e.getMessage() + ".");
}
}
```

## Alterações nos parâmetros de QOS {#changes-to-qos-parameters}

Há pequenas alterações nas propriedades do objeto QOSProvider:

* A variável `TimeToFirstFrame` O não está disponível no TVSDK 2.5.
* O TVSDK 2.5 QOSProvider tem uma nova propriedade para determinar a largura de banda percebida durante uma sessão de transmissão.

```java
//TVSDK v1.4
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitrate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); setQosItem("Time to first frame", (int) playbackInformation.getTimeToFirstFrame()); setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); setQosItem("Last seek time", (int) playbackInformation.getLastSeekTime());
}

//TVSDK v2.5
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitRate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart());
setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare());
setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());
```

* A variável `QOSEventListener::onOperationFailed()` não existe mais no TVSDK 2.5. Os avisos que costumavam aparecer neste ouvinte de eventos agora aparecerão no `NotificationEventListener::onNotification()` ouvinte de eventos.

* A variável `QOSProvider event listeners onBufferStart()`, `onBufferComplete()`, `onSeekStart()`, `onSeekComplete()`, e `onLoadInfo()` são ouvintes de eventos individuais vinculados a uma ocorrência de mediaPlayer.

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener() {

@Override
public void onBufferStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
@Override
public void onBufferComplete() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
hideBufferingSpinner();
}
@Override
public void onSeekStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
@Override
public void onSeekComplete(long adjustedTime) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " +
adjustedTime + ".");
_controlBar.setPosition(adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayer.PlayerState.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
@Override
public void onLoadInfo(LoadInfo loadInfo) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " +
loadInfo.getUrl() + ", size: " + loadInfo.getSize() +
" bytes, media duration: " +
loadInfo.getMediaDuration() + "ms, download duration: " +
loadInfo.getDownloadDuration() + "ms");
 
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - "). append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append(key).append(": ").
append(metadata.getValue(key));
}
}
innerNotification = innerNotification.getInnerNotification();
}
String errMsg = sb.toString(); PMPDemoApp.logger.w(LOG_TAG +
"::MediaPlayer.QOSEventListener#onOperationFailed()", errMsg);
showToast(errMsg);
}
};

//TVSDK v2.5
mediaPlayer.addEventListener(MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE,
loadInfoEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_BEGIN,
bufferingBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_END,
bufferingEndEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_BEGIN,
seekBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_END,
seekEndEventListener);
// Buffering events.
BufferingBeginEventListener bufferingBeginEventListener = new BufferingBeginEventListener() {
@Override
public void onBufferingBegin(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
};

BufferingEndEventListener bufferingEndEventListener = new BufferingEndEventListener() {
@Override
public void onBufferingEnd(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()",
"Buffering complete."); hideBufferingSpinner();
}
};

BufferPreparedEventListener bufferPreparedEventListener = new BufferPreparedEventListener() {
@Override
public void onBufferPrepared() {
}
};
// seek events.
SeekBeginEventListener seekBeginEventListener = new SeekBeginEventListener() {

@Override
public void onSeekBegin(SeekEvent seekEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
};
SeekEndEventListener seekEndEventListener = new SeekEndEventListener() {
@Override
public void onSeekEnd(SeekEvent seekEvent) {
double adjustedTime = seekEvent.getActualPosition();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
_controlBar.setPosition((long) adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayerStatus.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
};
/**
* LoadInformationEventListener that intercepts PSDK load info events
*/
private final LoadInformationEventListener loadInfoEventListener = new LoadInformationEventListener() {

@Override
public void onLoadInformation(LoadInformationEvent event) { LoadInformation loadInfo = event.getLoadInfomation(); PMPDemoApp.logger.i(
LOG_TAG + "::LoadInformationEventListener#onLoadInfomation()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize()
+ " bytes, download duration: "
+ loadInfo.getDownloadDuration() + "ms");
}
};
```

## Recursos úteis {#helpful-resources}

* Consulte a documentação de ajuda completa em [Aprendizagem e suporte do Adobe Primetime](https://helpx.adobe.com/support/primetime.html) página.
