---
description: Este exemplo mostra a maneira recomendada de incluir especificações de Intervalo de tempo na linha do tempo de reprodução.
title: Colocar marcadores de anúncio de Intervalo de Tempo na linha do tempo
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Colocar marcadores de anúncio de Intervalo de Tempo na linha do tempo {#place-timerange-ad-markers-on-the-timeline}

Este exemplo mostra a maneira recomendada de incluir especificações de Intervalo de tempo na linha do tempo de reprodução.

1. Traduza as informações de posicionamento de anúncios fora de banda em uma lista de `TimeRange` especificações (ou seja, instâncias da `TimeRange` classe).
1. Use o conjunto de `TimeRange` especificações para preencher uma instância do `TimeRangeCollection` classe.
1. Transmita a instância de metadados, que pode ser obtida do `TimeRangeCollection` instância, para o `replaceCurrentItem` (parte da interface do MediaPlayer).
1. Aguarde o TVSDK fazer a transição para o `PREPARED` ao aguardar o `PlaybackEventListener#onPrepared` retorno de chamada a ser acionado.
1. Inicie a reprodução de vídeo chamando o `play()` (parte da `MediaPlayer` interface).

* Resolução de conflitos de linha do tempo: pode haver casos em que alguns `TimeRange` as especificações se sobrepõem na linha do tempo de reprodução. Por exemplo, o valor da posição inicial correspondente a um `TimeRange` a especificação pode ser menor do que o valor da posição final que já foi colocada. Nesse caso, o TVSDK ajusta silenciosamente a posição inicial do infrator `TimeRange` para evitar conflitos de linha do tempo. Através deste ajustamento, o novo `TimeRange` torna-se mais curto do que o especificado originalmente. Se o ajustamento for tão extremo que conduza a uma `TimeRange` com uma duração de zero ms, o TVSDK ignora silenciosamente a `TimeRange` especificação.
* Quando `TimeRange` As especificações para ad breaks personalizados são fornecidas, o TVSDK tenta traduzi-los em anúncios que são agrupados dentro de ad breaks. O TVSDK procura por `TimeRange` especificações e os agrupa em ad breaks separados. Se houver intervalos de tempo que não sejam adjacentes a nenhum outro intervalo de tempo, eles serão traduzidos em ad breaks que contêm um único anúncio.
* Pressupõe-se que o item do reprodutor de mídia que está sendo carregado aponta para um ativo de VOD. O TVSDK verifica isso sempre que o aplicativo tenta carregar um recurso de mídia cujos metadados contêm `TimeRange` especificações que podem ser usadas somente no contexto do recurso ad-markers personalizado. Se o ativo subjacente não for do tipo VOD, a biblioteca TVSDK acionará uma exceção.
* Ao lidar com marcadores de anúncios personalizados, o TVSDK desativa outros mecanismos de resolução de anúncios (por meio do Adobe Primetime ad decisioning (anteriormente conhecido como Auditude) ou outro sistema de provisionamento de anúncios). Você pode usar um dos vários módulos ad-resolver fornecidos pelo TVSDK ou o mecanismo personalizado de marcadores de anúncios. Ao usar a API de marcadores de anúncios personalizados, o conteúdo do anúncio é considerado já resolvido e colocado na linha do tempo.

O trecho de código a seguir fornece um exemplo simples em que um conjunto de três especificações de Intervalo de tempo é colocado na linha do tempo como marcadores de anúncios personalizados.

```java>
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
TimeRangeCollection timeRanges = new TimeRangeCollection();  
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
 
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                               timeRanges.toMetadata(null)); 
 
// prepare the content for playback by creating 
// NOTE: mediaPlayer is an instance of a properly configured MediaPlayer  
mediaPlayer.replaceCurrentItem(mediaResource); 
// wait for TVSDK to reach the PREPARED state 
... 
MediaPlayer.PlaybackEventListener playbackEventListener = new 
  MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() { 
        // TVSDK in in the PREPARED state. We are allowed to start the playback  
        mediaPlayer.play(); 
    } 
} 
```
