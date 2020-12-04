---
description: Este exemplo mostra a maneira recomendada de incluir marcadores de anúncio personalizados na linha do tempo de reprodução.
seo-description: Este exemplo mostra a maneira recomendada de incluir marcadores de anúncio personalizados na linha do tempo de reprodução.
seo-title: Coloque marcadores de anúncio personalizados na linha do tempo
title: Coloque marcadores de anúncio personalizados na linha do tempo
uuid: ee74d1f3-7186-44b8-bad7-55af579842e8
translation-type: tm+mt
source-git-commit: 9f1f27bc6c23994338775a32f978a2e768a0f3aa
workflow-type: tm+mt
source-wordcount: '360'
ht-degree: 0%

---


# Coloque marcadores de anúncio personalizados na linha do tempo {#place-custom-ad-markers-on-the-timeline}

Este exemplo mostra a maneira recomendada de incluir marcadores de anúncio personalizados na linha do tempo de reprodução.

1. Traduza as informações de posicionamento de anúncios fora de banda em uma lista/matriz da classe `RepaceTimeRange`.
1. Crie uma instância da classe `CustomRangeMetadata` e use seu método `setTimeRangeList` com a lista/matriz como seu argumento para definir sua lista de intervalo de tempo.
1. Use seu método `setType` para definir o tipo como `MARK_RANGE`.
1. Use o método `MediaPlayerItemConfig.setCustomRangeMetadata` com a instância `CustomRangeMetadata` como seu argumento para definir os metadados do intervalo personalizado.
1. Use o método `MediaPlayer.replaceCurrentResource` com a instância `MediaPlayerItemConfig` como seu argumento para definir o novo recurso como o atual.
1. Aguarde um evento `STATE_CHANGED`, que informa que o player está no estado `PREPARED`.
1. Reprodução de vídeo de start ao chamar `MediaPlayer.play`.

Este é o resultado da conclusão das tarefas neste exemplo: >
* Se um `ReplaceTimeRange` sobrepor outro na linha do tempo de reprodução, por exemplo, a posição do start de um `ReplaceTimeRange` for anterior à posição final já colocada, o TVSDK ajusta silenciosamente o start do `ReplaceTimeRange` ofensivo para evitar o conflito.

   Isso faz com que o `ReplaceTimeRange` ajustado seja menor do que o especificado originalmente. Se o ajuste levar a uma duração de zero, o TVSDK solta silenciosamente o `ReplaceTimeRange` ofensivo.

* O TVSDK procura intervalos de tempo adjacentes para quebras de anúncio personalizadas e as agrupa em quebras de anúncio separadas.

   Os intervalos de tempo não adjacentes a qualquer outro intervalo de tempo são traduzidos em intervalos de anúncios que contêm um único anúncio.
* Se o aplicativo tentar carregar um recurso de mídia cuja configuração contenha `CustomRangeMetadata` que possa ser usado somente nos marcadores de anúncio personalizados de contexto, o TVSDK lançará uma exceção se o ativo subjacente não for do tipo VOD.
* Ao lidar com marcadores de anúncios personalizados, o TVSDK desativa outros mecanismos de resolução de anúncios (por exemplo, decisões de anúncios da Adobe Primetime).

   Você pode usar qualquer módulo TVSDK de resolução de anúncios ou o mecanismo personalizado de marcadores de anúncios. Quando você usa marcadores de anúncio personalizados, o conteúdo do anúncio é considerado resolvido e colocado na linha do tempo.

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
