---
description: Você pode obter uma descrição da linha do tempo associada ao item selecionado no momento que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizada no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
title: Inspect a linha do tempo da reprodução
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '205'
ht-degree: 0%

---


# Inspect a linha do tempo de reprodução{#inspect-the-playback-timeline}

Você pode obter uma descrição da linha do tempo associada ao item selecionado no momento que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizada no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.

Veja um exemplo de implementação como visto na seguinte captura de tela.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acesse o objeto `Timeline` no `MediaPlayer` usando o método `get`.

   A classe `Timeline` encapsula as informações relacionadas ao conteúdo da linha do tempo associado ao item de mídia que está carregado atualmente pela instância `MediaPlayer`. A classe `Timeline` fornece acesso a uma exibição somente leitura da linha do tempo subjacente. A classe `Timeline` fornece um método getter para obter todos os objetos `TimelineMarker` colocados.

1. Itere pela lista de `TimelineMarkers` e use as informações retornadas para implementar sua linha do tempo.

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

