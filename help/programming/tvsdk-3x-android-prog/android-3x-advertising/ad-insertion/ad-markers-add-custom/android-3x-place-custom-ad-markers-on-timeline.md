---
description: Este exemplo mostra a maneira recomendada de incluir marcadores de anúncios personalizados na linha do tempo de reprodução.
title: Colocar marcadores de anúncios personalizados na linha do tempo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---

# Colocar marcadores de anúncios personalizados na linha do tempo {#place-custom-ad-markers-on-the-timeline}

Este exemplo mostra a maneira recomendada de incluir marcadores de anúncios personalizados na linha do tempo de reprodução.

1. Traduza as informações de posicionamento de anúncios fora de banda em uma lista/matriz de `RepaceTimeRange` classe.
1. Criar uma instância de `CustomRangeMetadata` e use sua `setTimeRangeList` com a lista/matriz como seu argumento para definir sua lista de intervalo de tempo.
1. Use seus `setType` método para definir o tipo como `MARK_RANGE`.
1. Use o `MediaPlayerItemConfig.setCustomRangeMetadata` com o `CustomRangeMetadata` instância como seu argumento para definir os metadados de intervalo personalizado.
1. Use o `MediaPlayer.replaceCurrentResource` com o `MediaPlayerItemConfig` como seu argumento para definir, torne o novo recurso o atual.
1. Aguarde um `STATE_CHANGED` evento, que relata que o reprodutor está no estado `PREPARED` estado.
1. Iniciar reprodução de vídeo chamando `MediaPlayer.play`.

Este é o resultado da conclusão das tarefas neste exemplo:

* Se um `ReplaceTimeRange` sobrepõe outro na linha do tempo de reprodução, por exemplo, a posição inicial de um `ReplaceTimeRange` for anterior a uma posição final já colocada, o TVSDK ajusta silenciosamente o início do evento `ReplaceTimeRange` para evitar o conflito.

  Isso faz com que as `ReplaceTimeRange` mais curto do que o especificado originalmente. Se o ajuste levar a uma duração de zero, o TVSDK silenciosamente descartará o problema `ReplaceTimeRange`.

* O TVSDK procura intervalos de tempo adjacentes para ad breaks personalizados e os agrupa em ad breaks separados.

Intervalos de tempo não adjacentes a qualquer outro intervalo de tempo são traduzidos em ad breaks que contêm um único anúncio.

* Se o aplicativo tentar carregar um recurso de mídia cuja configuração contém `CustomRangeMetadata` que pode ser usado somente em marcadores de anúncios personalizados de contexto, o TVSDK aciona uma exceção se o ativo subjacente não for do tipo VOD.

* Ao lidar com marcadores de anúncios personalizados, o TVSDK desativa outros mecanismos de resolução de anúncios (por exemplo, o Adobe Primetime ad decisioning).

  Você pode usar qualquer módulo de ad-resolver TVSDK ou o mecanismo personalizado de marcadores de anúncios. Quando você usa marcadores de anúncio personalizados, o conteúdo do anúncio é considerado resolvido e é colocado na linha do tempo.

O trecho de código a seguir coloca três intervalos de tempo na linha do tempo como marcadores de anúncios personalizados.

```java
// Assume that the 3 time ranges are obtained through external means 
// Use them to populate the ReplaceTimeRange instance 
List<ReplaceTimeRange> timeRanges = new ArrayList<ReplaceTimeRange>(); 
timeRanges.add(new ReplaceTimeRange(0,10000, 0)); 
timeRanges.add(new ReplaceTimeRange(15000,20000, 0)); 
timeRanges.add(new ReplaceTimeRange(25000,30000, 0)); 
 
CustomRangeMetadata customRangeMetadata = new CustomRangeMetadata(); 
customRangeMetadata.setTimeRangeList(timeRanges); 
customRangeMetadata.setType(CustomRangeMetadata.CustomRangeType.MARK_RANGE); 
 
//Create a MediaResource instance 
MediaResource mediaResource = MediaResource.createFromUrl( 
        "www.example.com/video/test_video.m3u8", timeRanges.toMedatada(null)); 
 
// Create a MediaPlayerItemConfig instance 
MediaPlayerItemConfig config =  
  new MediaPlayerItemConfig(getActivity().getApplicationContext()); 
 
// Set customRangeMetadata 
config.setCustomRangeMetadata(customRangeMetadata); 
 
// Prepare the content for playback by calling replaceCurrentResource 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentResource(mediaResource, config); 
 
// wait for TVSDK to reach the PREPARED state 
mediaPlayer.addEventListener(MediaPlayerEvent.STATE_CHANGED,  
  new StatusChangeEventListener() { 
    @Override 
    public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
 
    if( event.getStatus() == MediaPlayerStatus.PREPARED ) { 
        // TVSDK is in the PREPARED state, so start the playback  
        mediaPlayer.play(); 
    } 
    ... 
}
```
