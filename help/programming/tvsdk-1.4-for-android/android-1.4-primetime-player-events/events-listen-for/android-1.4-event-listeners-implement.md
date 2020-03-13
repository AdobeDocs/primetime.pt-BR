---
description: Os manipuladores de eventos permitem que o TVSDK responda a eventos.
seo-description: Os manipuladores de eventos permitem que o TVSDK responda a eventos.
seo-title: Implementar ouvintes e retornos de chamada de evento
title: Implementar ouvintes e retornos de chamada de evento
uuid: 6b7859a4-55f9-48b1-b1f1-7b79bc92610a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Implementar ouvintes e retornos de chamada de evento{#implement-event-listeners-and-callbacks}

Os manipuladores de eventos permitem que o TVSDK responda a eventos.

Quando um evento ocorre, o mecanismo de evento do TVSDK chama seu manipulador de eventos registrado e transmite as informações do evento para o manipulador.

O TVSDK define os ouvintes como interfaces internas públicas na `MediaPlayer` interface.

Seu aplicativo deve implementar ouvintes de eventos para eventos TVSDK que afetam seu aplicativo.

Para obter uma lista completa dos eventos para análise de vídeo, consulte Monitoramento da reprodução de vídeo principal.

1. Determine para quais eventos seu aplicativo deve ouvir.

   * **Eventos** obrigatórios: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >O evento reproduzir `onStateChanged` fornece o estado do player, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do player

   * **Outros eventos**: Opcional, dependendo do aplicativo.

      Por exemplo, se você incorporar publicidade na reprodução, implemente os retornos de chamada AdPlaybackEventListener.

1. Implemente ouvintes de eventos para cada evento.

   O TVSDK retorna valores de parâmetro para os retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar em seus ouvintes para executar ações apropriadas.

   `MediaPlayer.EventListener` lista todas as interfaces de retorno de chamada. Cada interface exibe o nome e os parâmetros de retorno de chamada retornados para cada evento.

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

O TVSDK envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.

Os exemplos a seguir mostram a ordem de alguns eventos que incluem eventos de reprodução.

* Ao carregar com êxito um recurso de mídia por meio `MediaPlayer.replaceCurrentResource`, a ordem dos eventos é:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` estado `MediaPlayer.PlayerState.INITIALIZING`

1. `MediaPlayer.PlaybackEventListener.onStateChanged` estado `MediaPlayer.PlayerState.INITIALIZED`

>[!TIP]
>
>Carregue o recurso de mídia no thread principal. Se você carregar um recurso de mídia em um thread em segundo plano, essa operação ou as operações subsequentes do TVSDK, ou ambas, podem gerar um erro (por exemplo, `IllegalStateException`) e sair.

* Ao se preparar para a reprodução, `MediaPlayer.prepareToPlay`a ordem dos eventos é:

1. `MediaPlayer.PlaybackEventListener.onStateChanged` estado `MediaPlayerStatus.PREPARING`

1. `MediaPlayer.PlaybackEventListener.onTimelineUpdated` se as publicidades foram inseridas.
1. `MediaPlayer.PlaybackEventListener.onStateChanged` estado `MediaPlayerStatus.PREPARED`

* Para fluxos ao vivo/lineares, durante a reprodução à medida que a janela de reprodução avança e oportunidades adicionais são resolvidas, a ordem dos eventos é:

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

## Ordem dos eventos publicitários {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Quando a reprodução inclui publicidade, o TVSDK envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.

Ao reproduzir publicidades, a ordem dos eventos é:

* `AdPlaybackEventListener.onAdBreakStart`
* Os seguintes anúncios são enviados para cada anúncio no intervalo de anúncios:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (várias vezes durante a reprodução de um anúncio)
   * `AdPlaybackEventListener.onAdClick` (para cada clique)
   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdBreakComplete`

O exemplo a seguir mostra uma progressão típica dos eventos de reprodução de anúncio:

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

Ao reproduzir publicidades, a ordem dos eventos é:

* `AdPlaybackEventListener.onAdBreakStart`
* Os seguintes anúncios são enviados para cada anúncio no intervalo de anúncios:

   * `AdPlaybackEventListener.onAdStart`
   * `AdPlaybackEventListener.onAdProgress` (várias vezes durante a reprodução de um anúncio)
   * `AdPlaybackEventListener.onAdClick` (para cada clique)
   * `AdPlaybackEventListener.onAdStart`

* `AdPlaybackEventListener.onAdBreakComplete`

O exemplo a seguir mostra uma progressão típica dos eventos de reprodução de anúncio:

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

O TVSDK despacha eventos de qualidade de serviço (QoS) para notificar seu aplicativo sobre eventos que podem influenciar o cálculo das estatísticas de QoS, como eventos de buffering e busca.

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

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis. O player pode implementar ações em resposta a esses eventos.

Para ser notificado sobre todos os eventos relacionados ao DRM, ouça `onDRMMetadata(DRMMetadataInfo drmMetadataInfo)`. O TVSDK envia eventos DRM adicionais por meio da `DRMManager` classe.

O exemplo a seguir mostra uma progressão típica:

```
mediaPlayer.addEventListener(MediaPlayer.Event.DRM, 
 new MediaPlayer.DRMEventListener() { 
 @Override 
 public void onDRMMetadata(byte[] data, int length, long timestamp) {...} 
}); 
```

## Eventos de carregador {#section_5638F8EDACCE422A9425187484D39DCC}

O player pode implementar ações com base nos seguintes eventos:

| Evento | Significado |
|---|---|
| `onLoadComplete (mediaPlayerItem playerItem)` | O carregamento do recurso de mídia foi concluído com êxito. |
| `onError` | Ocorreu um problema com o carregamento de recursos de mídia. |

