---
description: Você pode obter uma descrição da linha do tempo associada ao item selecionado no momento que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizada no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
title: Inspect a linha do tempo da reprodução
exl-id: 38b5ce0e-5554-462e-986f-f3864f7cf879
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Inspect a linha do tempo da reprodução{#inspect-the-playback-timeline}

Você pode obter uma descrição da linha do tempo associada ao item selecionado no momento que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizada no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.

Veja um exemplo de implementação como visto na seguinte captura de tela.
<!--<a id="fig_6D9FB3764F3947A38B8E7726187BD461"></a>-->

![](assets/inspect-playback.jpg){width="368.641pt"}

1. Acesse o `Timeline` na `MediaPlayer` usando o `get` método .

   O `Timeline` encapsula as informações relacionadas ao conteúdo da linha do tempo associado ao item de mídia que está carregado atualmente pela variável `MediaPlayer` instância. O `Timeline` fornece acesso a uma exibição somente leitura da linha do tempo subjacente. O `Timeline` classe fornece um método getter para obter todos os `TimelineMarker` objetos.

1. Iterar pela lista de `TimelineMarkers` e use as informações retornadas para implementar sua linha do tempo.

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
