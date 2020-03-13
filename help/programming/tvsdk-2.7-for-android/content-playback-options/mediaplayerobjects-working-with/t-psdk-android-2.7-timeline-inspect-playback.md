---
description: Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
seo-description: Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
seo-title: Inspecione a linha do tempo de reprodução
title: Inspecione a linha do tempo de reprodução
uuid: d0fe7926-9b9a-4203-a1c7-e57ba25b882e
translation-type: tm+mt
source-git-commit: 0eaf0e7e7e61d596a51d1c9c837ad072d703c6a7

---


# Inspecione a linha do tempo de reprodução {#inspect-the-playback-timeline}

Você pode obter uma descrição da linha do tempo associada ao item atualmente selecionado que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizado no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.

Este é um exemplo de implementação, como visto na seguinte captura de tela.  ![](assets/inspect-playback.jpg){width=&quot;368.641pt&quot;}

1. Acesse o `Timeline` objeto no `MediaPlayer` usando o `getTimeline()` método.

   A `Timeline` classe encapsula as informações relacionadas ao conteúdo da linha do tempo que está associado ao item de mídia que está carregado atualmente pela `MediaPlayer` instância. A `Timeline` classe fornece acesso a uma exibição somente leitura da linha do tempo subjacente. A `Timeline` classe fornece um método getter que fornece um iterador por meio de uma lista de `TimelineMarker` objetos.

1. Iterar pela lista de `TimelineMarkers` e usar as informações retornadas para implementar sua linha do tempo.

       Um objeto &quot;TimelineMarker&quot; contém duas informações:
   
   * Posição do marcador na linha do tempo (em milissegundos)
   * Duração do marcador na linha do tempo (em milissegundos)

1. Analise o `MediaPlayerEvent.TIMELINE_UPDATED` evento na `MediaPlayer` instância e implemente o `TimelineUpdatedEventListener.onTimelineUpdated()` retorno de chamada.

   O `Timeline` objeto pode informar seu aplicativo sobre alterações que podem ocorrer na linha do tempo de reprodução chamando seu `OnTimelineUpdated` ouvinte.

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
