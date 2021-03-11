---
description: Este exemplo mostra a maneira recomendada de incluir marcadores de anúncio personalizados na linha do tempo da reprodução.
title: Inserir marcadores de anúncio personalizados na linha do tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Inserir marcadores de anúncio personalizados na linha do tempo {#place-custom-ad-markers-on-the-timeline}

Este exemplo mostra a maneira recomendada de incluir marcadores de anúncio personalizados na linha do tempo da reprodução.

1. Traduza as informações de posicionamento de anúncios fora de banda em uma lista/matriz de classe `RepaceTimeRange`.
1. Crie uma instância da classe `CustomRangeMetadata` e use seu método `setTimeRangeList` com a lista/matriz como seu argumento para definir sua lista de intervalo de tempo.
1. Use o método `setType` para definir o tipo como `MARK_RANGE`.
1. Use o método `MediaPlayerItemConfig.setCustomRangeMetadata` com a instância `CustomRangeMetadata` como seu argumento para definir os metadados de intervalo personalizados.
1. Use o método `MediaPlayer.replaceCurrentResource` com a instância `MediaPlayerItemConfig` como seu argumento para definir tornar o novo recurso o atual.
1. Aguarde um evento `STATE_CHANGED`, que informa que o reprodutor está no estado `PREPARED`.
1. Inicie a reprodução do vídeo, chamando `MediaPlayer.play`.

Este é o resultado da conclusão das tarefas neste exemplo: >
* Se um `ReplaceTimeRange` se sobrepõe a outro na linha do tempo de reprodução, por exemplo, a posição inicial de um `ReplaceTimeRange` é anterior a uma posição final já colocada, o TVSDK ajusta silenciosamente o início do `ReplaceTimeRange` incorreto para evitar o conflito.

   Isso torna o `ReplaceTimeRange` ajustado menor do que o especificado originalmente. Se o ajuste levar a uma duração de zero, o TVSDK ignora silenciosamente o `ReplaceTimeRange` incorreto.

* O TVSDK busca intervalos de tempo adjacentes para ad breaks personalizados e os agrupa em ad breaks separados.

   Intervalos de tempo não adjacentes a qualquer outro intervalo de tempo são traduzidos em ad breaks que contêm um único anúncio.
* Se o aplicativo tentar carregar um recurso de mídia cuja configuração contenha `CustomRangeMetadata` que pode ser usado somente nos marcadores de anúncio personalizados de contexto, o TVSDK acionará uma exceção se o ativo subjacente não for do tipo VOD.
* Ao lidar com marcadores de anúncios personalizados, o TVSDK desativa outros mecanismos de resolução de anúncios (por exemplo, Adobe Primetime ad decisioning).

   Você pode usar qualquer módulo de resolvedor de anúncios TVSDK ou o mecanismo de marcadores de anúncios personalizados. Quando você usa marcadores de anúncios personalizados, o conteúdo do anúncio é considerado resolvido e colocado na linha do tempo.

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
