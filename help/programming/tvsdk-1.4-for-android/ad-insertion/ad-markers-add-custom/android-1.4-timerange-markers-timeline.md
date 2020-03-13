---
description: Este exemplo mostra a maneira recomendada de incluir especificações de TimeRange na linha do tempo de reprodução.
seo-description: Este exemplo mostra a maneira recomendada de incluir especificações de TimeRange na linha do tempo de reprodução.
seo-title: Colocar marcadores de intervalo de tempo na linha do tempo
title: Colocar marcadores de intervalo de tempo na linha do tempo
uuid: 12935eba-2e91-40ea-a60e-02d0060c3cce
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Colocar marcadores de intervalo de tempo na linha do tempo {#place-timerange-ad-markers-on-the-timeline}

Este exemplo mostra a maneira recomendada de incluir especificações de TimeRange na linha do tempo de reprodução.

1. Traduza as informações de posicionamento de anúncios fora de banda em uma lista de `TimeRange` especificações (isto é, instâncias da `TimeRange` classe).
1. Use o conjunto de `TimeRange` especificações para preencher uma instância da `TimeRangeCollection` classe.
1. Passe a instância Metadata, que pode ser obtida da `TimeRangeCollection` instância, para o `replaceCurrentItem` método (parte da interface do MediaPlayer).
1. Aguarde a transição do TVSDK para o `PREPARED` estado aguardando o `PlaybackEventListener#onPrepared` retorno de chamada ser acionado.
1. Inicie a reprodução do vídeo chamando o `play()` método (parte da `MediaPlayer` interface).

* Tratamento de conflitos de linha do tempo: Pode haver casos em que algumas `TimeRange` especificações se sobrepõem na linha do tempo de reprodução. Por exemplo, o valor da posição inicial correspondente a uma `TimeRange` especificação pode ser inferior ao valor da posição final que já foi colocada. Nesse caso, o TVSDK ajusta silenciosamente a posição inicial da especificação `TimeRange` ofensiva para evitar conflitos de linha do tempo. Com este ajuste, o novo `TimeRange` torna-se mais curto do que o originalmente especificado. Se o ajuste for tão extremo que resultaria em um `TimeRange` com duração de zero ms, o TVSDK ignora silenciosamente a `TimeRange` especificação ofensiva.
* Quando são fornecidas `TimeRange` especificações para quebras de anúncio personalizadas, o TVSDK tenta traduzi-las em anúncios que são agrupados dentro de quebras de anúncio. O TVSDK procura `TimeRange` especificações adjacentes e as agrupa em quebras de anúncios separadas. Se houver intervalos de tempo que não sejam adjacentes a qualquer outro intervalo de tempo, eles serão traduzidos em intervalos de anúncios que contêm um único anúncio.
* Pressupõe-se que o item do player de mídia que está sendo carregado aponte para um ativo VOD. O TVSDK verifica isso sempre que seu aplicativo tenta carregar um recurso de mídia cujos metadados contêm `TimeRange` especificações que podem ser usadas somente no contexto do recurso personalizado de marcadores de anúncios. Se o ativo subjacente não for do tipo VOD, a biblioteca TVSDK lançará uma exceção.
* Ao lidar com marcadores de anúncios personalizados, o TVSDK desativa outros mecanismos de resolução de anúncios (por meio da decisão do anúncio do Adobe Primetime (anteriormente conhecido como Auditude) ou de outro sistema de provisionamento de anúncios). Você pode usar um dos vários módulos de resolução de anúncios fornecidos pelo TVSDK ou o mecanismo personalizado de marcadores de anúncios. Ao usar a API personalizada de marcadores de anúncios, o conteúdo do anúncio é considerado já resolvido e colocado na linha do tempo.

O trecho de código a seguir fornece um exemplo simples onde um conjunto de três especificações TimeRange são colocadas na linha do tempo como marcadores de anúncios personalizados.

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
