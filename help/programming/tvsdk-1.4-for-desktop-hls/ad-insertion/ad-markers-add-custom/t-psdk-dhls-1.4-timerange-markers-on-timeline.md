---
description: Este exemplo mostra a maneira recomendada de incluir especificações de TimeRange na linha do tempo de reprodução.
seo-description: Este exemplo mostra a maneira recomendada de incluir especificações de TimeRange na linha do tempo de reprodução.
seo-title: Colocar marcadores de intervalo de tempo na linha do tempo
title: Colocar marcadores de intervalo de tempo na linha do tempo
uuid: cbcc4c84-0d56-4331-b555-b8e59f7d52d4
translation-type: tm+mt
source-git-commit: fd21a29bb186238142d43e0277bbf92f8406f6f7
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---


# Coloque os marcadores de intervalo de tempo na linha do tempo {#place-timerange-ad-markers-on-the-timeline}

Este exemplo mostra a maneira recomendada de incluir especificações de TimeRange na linha do tempo de reprodução.

1. Traduza as informações de posicionamento de anúncios fora de banda em uma lista de `TimeRange` especificações (ou seja, instâncias da classe `TimeRange`).
1. Use o conjunto de especificações `TimeRange` para preencher uma instância da classe `TimeRangeCollection`.
1. Passe a instância Metadados, que pode ser obtida da instância `TimeRangeCollection`, para o método `replaceCurrentItem` (parte da interface `MediaPlayer`).
1. Aguarde a transição do TVSDK para o estado PREPARADO aguardando o retorno de chamada `PlaybackEventListener#onPrepared` ser acionado.
1. Reprodução de vídeo de start chamando o método `play()` (parte da interface `MediaPlayer`).

* Tratamento de conflitos de linha do tempo: Pode haver casos em que algumas especificações `TimeRange` se sobrepõem na linha do tempo de reprodução. Por exemplo, o valor da posição do start correspondente a uma especificação `TimeRange` pode ser menor que o valor da posição final que já foi colocada. Nesse caso, o TVSDK ajusta silenciosamente a posição do start da especificação `TimeRange` ofensiva para evitar conflitos de linha do tempo. Por meio desse ajuste, o novo `TimeRange` se torna menor do que o especificado originalmente. Se o ajuste for tão extremo que resultaria em `TimeRange` com uma duração de zero ms, o TVSDK soltará silenciosamente a especificação `TimeRange` ofensiva.

* Quando `TimeRange` especificações para quebras de anúncios personalizadas são fornecidas, o TVSDK tenta traduzi-las em anúncios que são agrupados dentro de quebras de anúncios. O TVSDK procura especificações `TimeRange` adjacentes e as agrupa em quebras de anúncios separadas. Se houver intervalos de tempo que não sejam adjacentes a qualquer outro intervalo de tempo, eles serão traduzidos em intervalos de anúncios que contêm um único anúncio.

* Pressupõe-se que o item do player de mídia que está sendo carregado aponte para um ativo VOD. O TVSDK verifica isso sempre que seu aplicativo tenta carregar um recurso de mídia cujos metadados contêm `TimeRange` especificações que podem ser usadas somente no contexto do recurso personalizado de marcadores de anúncios. Se o ativo subjacente não for do tipo VOD, a biblioteca TVSDK lançará uma exceção.

* Ao lidar com marcadores de anúncios personalizados, o TVSDK desativa outros mecanismos de resolução de anúncios (via decisão de anúncios do Adobe Primetime (anteriormente conhecido como Auditude) ou outro sistema de provisionamento de anúncios). Você pode usar um dos vários módulos de resolução de anúncios fornecidos pelo TVSDK ou o mecanismo personalizado de marcadores de anúncios. Ao usar a API personalizada de marcadores de anúncios, o conteúdo do anúncio é considerado já resolvido e colocado na linha do tempo.

<!--<a id="example_639BD1B66CE74F3DB65ED06CAD23EB09"></a>-->

O trecho de código a seguir fornece um exemplo simples onde um conjunto de três `TimeRange` especificações é colocado na linha do tempo como marcadores de anúncio personalizados.

```
// Assume that the 3 timerange specs are obtained through external means: CMS, etc. 
// Use these 3 timerange specs to populate the TimeRangeCollection instance 
var timeRanges:TimeRangeCollection = new TimeRangeCollection(); 
timeRanges.addTimeRange(new TimeRange(0,10000)); 
timeRanges.addTimeRange(new TimeRange(15000,20000)); 
timeRanges.addTimeRange(new TimeRange(25000,30000)); 
  
// create and configure a MediaResource instance 
MediaResource mediaResource =  
  MediaResource.createFromUrl("www.example.com/video/test_video.m3u8",  
                             timeRanges.toMetadata(null));
```
