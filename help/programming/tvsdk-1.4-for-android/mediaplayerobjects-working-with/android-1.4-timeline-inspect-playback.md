---
description: Você pode obter uma descrição da linha do tempo associada ao item selecionado no momento que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizada no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.
title: Inspect a linha do tempo da reprodução
exl-id: af373f1e-ed5b-40a9-a91e-9eb0e4a181de
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 0%

---

# Inspect a linha do tempo da reprodução{#inspect-the-playback-timeline}

Você pode obter uma descrição da linha do tempo associada ao item selecionado no momento que está sendo reproduzido pelo TVSDK. Isso é mais útil quando seu aplicativo exibe um controle de barra de depuração personalizada no qual as seções de conteúdo que correspondem ao conteúdo do anúncio são identificadas.

Veja um exemplo de implementação como visto na seguinte captura de tela.  ![](assets/inspect-playback.jpg){width="368.641pt"}

1. Acesse o `Timeline` na `MediaPlayer` usando o `getTimeline` método .

   O `Timeline` encapsula as informações relacionadas ao conteúdo da linha do tempo associado ao item de mídia que está carregado atualmente pela variável `MediaPlayer` instância. O `Timeline` fornece acesso a uma exibição somente leitura da linha do tempo subjacente. O `Timeline` fornece um método getter que fornece um iterador por meio de uma lista de `TimelineMarker` objetos.

1. Iterar pela lista de `TimelineMarkers` e use as informações retornadas para implementar sua linha do tempo.

       Um objeto &quot;TimelineMarker&quot; contém duas informações:
   
   * Posição do marcador na linha do tempo (em milissegundos)
   * Duração do marcador na linha do tempo (em milissegundos)

1. Implementar a interface de retorno de chamada do ouvinte `MediaPlayer.PlaybackEventListener.onTimelineUpdated` e registrá-lo com o `Timeline` objeto.

   O `Timeline` O objeto pode informar seu aplicativo sobre alterações que podem ocorrer na linha do tempo de reprodução, chamando seu `OnTimelineUpdated` ouvinte.

```java
// access the timeline object 
Timeline timeline = mediaPlayer.getTimeline(); 
// iterate through the list of TimelineMarkers 
Iterator<TimelineMarker> iterator = timeline.timelineMarkers(); 
while (iterator.hasNext()) { 
   TimelineMarker marker = iterator.next(); 
   // the start position of the marker 
   long startPos = marker.getTime(); 
   // the duration of the marker 
   long duration = marker.getDuration(); 
}
```
