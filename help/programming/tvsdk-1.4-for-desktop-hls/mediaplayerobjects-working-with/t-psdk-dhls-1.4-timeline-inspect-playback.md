---
description: Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
seo-description: Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
seo-title: Inspecione a linha do tempo de reprodução
title: Inspecione a linha do tempo de reprodução
uuid: 2f903493-2d88-4af2-ac71-36300b49735b
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e

---


# Inspecione a linha do tempo de reprodução{#inspect-the-playback-timeline}

Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.

Este é um exemplo de implementação, como visto na seguinte captura de tela.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acesse o `Timeline` objeto no `MediaPlayer` usando o `get` método.

   A `Timeline` classe encapsula as informações relacionadas ao conteúdo da linha do tempo que está associado ao item de mídia que está carregado atualmente pela `MediaPlayer` instância. A `Timeline` classe fornece acesso a uma exibição somente leitura da linha do tempo subjacente. A `Timeline` classe fornece um método getter para obter todos os `TimelineMarker` objetos inseridos.

1. Iterar pela lista de `TimelineMarkers` e usar as informações retornadas para implementar sua linha do tempo.

       Um objeto &quot;TimelineMarker&quot; contém duas informações:
   
   * Posição do marcador na linha do tempo (em milissegundos)
   * Duração do marcador na linha do tempo (em milissegundos)

<!--<a id="example_BA936629E82B4082A2E2C548E3FC3357"></a>-->

```
// access the timeline object 
var timeline:Timeline = mediaPlayer.timeline; 
 
// iterate through the list of TimelineMarkers 
var markers:Vector.<TimelineMarker> = timeline.timelineMarkers; 
markers.forEach(function(item:TimelineMarker,  
                         index:int,  
                         vector:Vector.<TimelineMarker>):void { 
    
    // the start position of the marker 
    var startPos:Number = item.time; 
 
    // the duration of the marker 
    var duration:Number = item.duration; 
 
    // draw the marker on the scrub-bar 
}
```

