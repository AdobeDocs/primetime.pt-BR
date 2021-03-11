---
description: Este exemplo mostra a maneira recomendada de incluir especificações de Intervalo de tempo na linha do tempo de reprodução.
title: Inserir marcadores de anúncio de Intervalo de tempo na linha do tempo
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---


# Inserir marcadores de anúncio de Intervalo de tempo na linha do tempo {#place-timerange-ad-markers-on-the-timeline}

Este exemplo mostra a maneira recomendada de incluir especificações de Intervalo de tempo na linha do tempo de reprodução.

1. Traduza as informações de posicionamento de anúncios fora de banda em uma lista de `TimeRange` especificações (ou seja, instâncias da classe `TimeRange`).
1. Use o conjunto de `TimeRange` especificações para preencher uma instância da classe `TimeRangeCollection`.
1. Passe a instância Metadados, que pode ser obtida da instância `TimeRangeCollection`, para o método `replaceCurrentItem` (parte da interface MediaPlayer).
1. Aguarde o TVSDK fazer a transição para o estado `PREPARED` aguardando o retorno de chamada `PlaybackEventListener#onPrepared` ser acionado.
1. Inicie a reprodução do vídeo, chamando o método `play()` (parte da interface `MediaPlayer`).

* Lidar com conflitos de linha do tempo: Pode haver casos em que algumas especificações `TimeRange` se sobrepõem na linha do tempo da reprodução. Por exemplo, o valor da posição inicial correspondente a uma especificação `TimeRange` pode ser menor que o valor da posição final que já foi colocada. Nesse caso, o TVSDK ajusta silenciosamente a posição inicial da especificação `TimeRange` ofensiva para evitar conflitos de linha do tempo. Por meio desse ajuste, o novo `TimeRange` se torna menor do que o especificado originalmente. Se o ajuste for tão extremo que levaria a um `TimeRange` com uma duração de zero ms, o TVSDK ignora silenciosamente a especificação `TimeRange` ofensiva.
* Quando `TimeRange` especificações para ad breaks personalizados são fornecidas, o TVSDK tenta traduzi-las em anúncios que são agrupados dentro de ad breaks. O TVSDK procura especificações `TimeRange` adjacentes e as agrupa em quebras de anúncios separadas. Se houver intervalos de tempo não adjacentes a qualquer outro intervalo de tempo, eles serão traduzidos em intervalos de anúncios que contêm um único anúncio.
* Pressupõe-se que o item do reprodutor de mídia que está sendo carregado aponte para um ativo VOD. O TVSDK verifica isso sempre que seu aplicativo tenta carregar um recurso de mídia cujos metadados contêm `TimeRange` especificações que podem ser usadas somente no contexto do recurso de marcadores de anúncios personalizados. Se o ativo subjacente não for do tipo VOD, a biblioteca TVSDK lançará uma exceção.
* Ao lidar com marcadores de anúncios personalizados, o TVSDK desativa outros mecanismos de resolução de anúncios (por meio do Adobe Primetime ad decisioning (anteriormente conhecido como Auditude) ou de outro sistema de provisionamento de anúncios). Você pode usar um dos vários módulos de resolvedor de anúncios fornecidos pelo TVSDK ou o mecanismo personalizado de marcadores de anúncios. Ao usar a API personalizada de marcadores de anúncios, o conteúdo do anúncio é considerado já resolvido e colocado na linha do tempo.

O trecho de código a seguir fornece um exemplo simples em que um conjunto de três especificações de Intervalo de tempo são colocadas na linha do tempo como marcadores de anúncios personalizados.

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
