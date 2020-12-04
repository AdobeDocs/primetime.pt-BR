---
description: Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
seo-description: Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
seo-title: Inspect na linha do tempo da reprodução
title: Inspect na linha do tempo da reprodução
uuid: d5d68684-d658-44bc-bfff-952b7946c7fd
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '285'
ht-degree: 0%

---


# Inspect a linha do tempo de reprodução {#inspect-the-playback-timeline}

Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.

Este é um exemplo de implementação, como visto na seguinte captura de tela.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acesse o objeto `Timeline` em `MediaPlayer` usando o método `getTimeline()`.

   A classe `Timeline` encapsula as informações relacionadas ao conteúdo da linha do tempo que está associado ao item de mídia que está carregado atualmente pela instância `MediaPlayer`. A classe `Timeline` fornece acesso a uma visualização somente leitura da linha do tempo subjacente. A classe `Timeline` fornece um método getter que fornece um iterador por meio de uma lista de objetos `TimelineMarker`.

1. Itere pela lista de `TimelineMarkers` e use as informações retornadas para implementar sua linha do tempo.

       Um objeto &quot;TimelineMarker&quot; contém duas informações:
   
   * Posição do marcador na linha do tempo (em milissegundos)
   * Duração do marcador na linha do tempo (em milissegundos)

1. Analise o evento `MediaPlayerEvent.TIMELINE_UPDATED` na instância `MediaPlayer` e implemente o retorno de chamada `TimelineUpdatedEventListener.onTimelineUpdated()`.

   O objeto `Timeline` pode informar seu aplicativo sobre as alterações que podem ocorrer na linha do tempo de reprodução, chamando seu ouvinte `OnTimelineUpdated`.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
 
// Iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
 
while (iterator.hasNext()) { 
    TimelineMarker marker = iterator.next(); 
    // the start position of the marker 
    long startPos = marker.getTime(); 
    // the duration of the marker 
    long duration = marker.getDuration(); 
}
```
