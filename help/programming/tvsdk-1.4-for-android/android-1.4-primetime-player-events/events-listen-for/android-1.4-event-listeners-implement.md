---
description: Os manipuladores de eventos permitem que o TVSDK responda aos eventos.
title: Implementar ouvintes e retornos de chamada de evento
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '572'
ht-degree: 0%

---

# Implementar ouvintes e retornos de chamada de evento{#implement-event-listeners-and-callbacks}

Os manipuladores de eventos permitem que o TVSDK responda aos eventos.

Quando um evento ocorre, o mecanismo de eventos do TVSDK chama o manipulador de eventos registrado e transmite as informações do evento para o manipulador.

O TVSDK define ouvintes como interfaces internas públicas na `MediaPlayer` interface.

Seu aplicativo deve implementar ouvintes de eventos para eventos TVSDK que afetam seu aplicativo.

Para obter uma lista completa dos eventos de análise de vídeo, consulte Rastrear reprodução de vídeo principal.

1. Determine para quais eventos seu aplicativo deve ouvir.

   * **Eventos obrigatórios**: Analise todos os eventos de reprodução.

     >[!IMPORTANT]
     >
     >O evento de reprodução `onStateChanged` O fornece o estado do player, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do reprodutor

   * **Outros eventos**: opcional, dependendo do aplicativo.

     Por exemplo, se você incorporar publicidade em sua reprodução, implemente os retornos de chamada AdPlaybackEventListener.

1. Implemente ouvintes de eventos para cada evento.

   O TVSDK retorna valores de parâmetro para os retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar nos ouvintes para executar as ações apropriadas.

   `MediaPlayer.EventListener` lista todas as interfaces de retorno de chamada. Cada interface exibe o nome do retorno de chamada e os parâmetros retornados para cada evento.

   Por exemplo:

   ```
   MediaPlayer.PlaybackEventListener.onStateChanged( 
    MediaPlayer.PlayerState state, MediaPlayerNotification notification)
   ```

1. Registre seus ouvintes de retorno de chamada com o `MediaPlayer` objeto usando `MediaPlayer.addEventListener`.

   ```
   mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, 
    new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onStateChanged( 
    MediaPlayer.PlayerState state, 
    MediaPlayerNotification notification) {...} 
   }
   ```

## Ordem dos eventos de reprodução {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

O TVSDK despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.

Os exemplos a seguir mostram a ordem de alguns eventos que incluem eventos de reprodução.

* Ao carregar um recurso de mídia com êxito por meio do `MediaPlayer.replaceCurrentResource`, a ordem dos eventos é:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` com estado `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` com estado `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>Carregue o recurso de mídia no thread principal. Se você carregar um recurso de mídia em um thread em segundo plano, essa operação ou operações subsequentes do TVSDK, ou ambas, poderão gerar um erro (por exemplo, `IllegalStateException`) e saia.

* Ao se preparar para a reprodução por meio do `MediaPlayer.prepareToPlay`, a ordem dos eventos é:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` com estado `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` se anúncios foram inseridos.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` com estado `MediaPlayerStatus.PREPARED`

* Para fluxos ao vivo/lineares, durante a reprodução, à medida que a janela de reprodução avança e as oportunidades adicionais são resolvidas, a ordem dos eventos é:

1. `MediaPlayer.PlaybackEventListener.onUpdated`
1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` se anúncios foram inseridos
1. `MediaPlayerItemEvent.ITEM_UPDATED`
1. `TimelineEvent.TIMELINE_UPDATED` se anúncios foram inseridos

O exemplo a seguir mostra uma progressão típica de eventos:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.PLAYBACK,  
  new MediaPlayer.PlaybackEventListener() { 
    @Override 
    public void onPrepared() {...} 
    @Override 
    public void onUpdated() {...} 
    @Override 
    public void onPlayStart() {...} 
    @Override 
    public void onPlayComplete() {...} 
    @Override 
    public void onSizeAvailable(long height, long width) {...} 
    @Override 
    public void onStateChanged(MediaPlayer.PlayerState state,  
      MediaPlayerNotification notification) {...} 
});
```

## Ordem dos eventos de publicidade {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Quando a reprodução inclui publicidade, o TVSDK despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.

Ao reproduzir anúncios, a ordem dos eventos é:

* `AdPlaybackEventListener.onAdBreakStart`
* Os itens a seguir são despachados para cada anúncio no ad break:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (várias vezes durante a reprodução de um anúncio)
   * `AdPlaybackEventListener.onAdClick` (para cada clique)
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

O exemplo a seguir mostra uma progressão típica de eventos de reprodução de anúncio:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

Ao reproduzir anúncios, a ordem dos eventos é:

* `AdPlaybackEventListener.onAdBreakStart`
* Os itens a seguir são despachados para cada anúncio no ad break:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (várias vezes durante a reprodução de um anúncio)
   * `AdPlaybackEventListener.onAdClick` (para cada clique)
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

O exemplo a seguir mostra uma progressão típica de eventos de reprodução de anúncio:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.AD_PLAYBACK,  
  new MediaPlayer.AdPlaybackEventListener() { 
    @Override  
    public void onAdBreakStart(AdBreak adBreak) { ... } 
    @Override 
    public void onAdStart(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdProgress(AdBreak adBreak, Ad ad, int percentage) { ... }  
    @Override 
    public void onAdComplete(AdBreak adBreak, Ad ad) { ... } 
    @Override 
    public void onAdBreakComplete(AdBreak adBreak) { ... } 
    @Override 
    public void onAdClick(AdBreak adBreak, Ad ad, AdClick adClick) { ... } 
});
```

## Eventos de QoS {#section_9BFF3CD7AA1C4BD6960ACF6B9C0B25CC}

O TVSDK despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como buffering e eventos de busca.

O exemplo a seguir mostra uma progressão típica desses eventos:

```java
mediaPlayer.addEventListener(MediaPlayer.Event.QOS,  
  new MediaPlayer.QOSEventListener(){ 
    //For buffering activity 
    @Override 
    public void onBufferStart() 
    @Override 
    public void onBufferComplete() 
    // For seeking 
    @Override 
    public void onSeekStart() 
    @Override 
    public void onSeekComplete(long adjustedTime) 
    @Override 
    public void onLoadComplete (MediaPlayerItem mediaplayeritem) 
    @Override 
    public void onLoadInfo(LoadInfo loadInfo) 
    @Override 
    public void onOperationFailed(MediaPlayerNotification.Warning warning) 
});
```

## Eventos DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados de DRM são disponibilizados. Seu reprodutor pode implementar ações em resposta a esses eventos.

Para ser notificado sobre todos os eventos relacionados ao DRM, acompanhe `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. O TVSDK despacha eventos DRM adicionais por meio da `DRMManager` classe.

O exemplo a seguir mostra uma progressão típica:

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## Eventos carregadores {#section_5638F8EDACCE422A9425187484D39DCC}

Seu reprodutor pode implementar ações com base nos seguintes eventos:

| Evento | Significado |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | O carregamento do recurso de mídia foi concluído com êxito. |
| `onError` | Ocorreu um problema com o carregamento do recurso de mídia. |
