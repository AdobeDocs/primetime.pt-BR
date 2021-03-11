---
description: Os manipuladores de eventos permitem que você responda a eventos TVSDK.
title: Implementar ouvintes e retornos de chamada do evento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '448'
ht-degree: 0%

---


# Implementar ouvintes de eventos e retornos de chamada {#implement-event-listeners-and-callbacks}

Os manipuladores de eventos permitem que você responda a eventos TVSDK.

Quando um evento ocorre, o mecanismo de evento do TVSDK chama o manipulador de evento registrado, transmitindo as informações do evento.

O TVSDK define ouvintes como interfaces internas públicas dentro da interface `MediaPlayer`.

Seu aplicativo deve implementar ouvintes de eventos para qualquer evento TVSDK que afete seu aplicativo.

1. Determine quais eventos seu aplicativo deve acompanhar.

   * Eventos obrigatórios: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >Analise o evento de alteração de status, que ocorre quando o status do reprodutor muda de maneiras que você precisa saber. As informações fornecidas incluem erros que podem afetar o que o reprodutor pode fazer em seguida.

   * Para outros eventos, dependendo do aplicativo, consulte [Resumo dos eventos do player do Primetime](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

1. Implemente e adicione um ouvinte de evento para cada evento.

   Para a maioria dos eventos, o TVSDK transmite argumentos para os ouvintes do evento. Esses valores fornecem informações sobre o evento que pode ajudá-lo a decidir o que fazer em seguida. A enumeração `MediaPlayerEvent` lista todos os eventos que `MediaPlayer` despacha. Para obter mais informações, consulte [Resumo dos eventos do player do Primetime](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   Por exemplo, se `mPlayer` for uma instância de `MediaPlayer`, é possível adicionar e estruturar um ouvinte de evento:

   ```java
   mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() { 
       @Override 
       public void onStatusChanged(MediaPlayerStatusChangeEvent event) { 
           event.getMetadata(); 
           if (event.getMetadata() != null) {/* Do something */} 
           if (event.getStatus() == MediaPlayerStatus.IDLE) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.INITIALIZED) {/* Do something */} 
           else if (event.getStatus() == MediaPlayerStatus.PREPARED) {/* Do something */} 
       } 
   }); 
   ```

## Ordem dos eventos de reprodução {#section_6D412C33ACE54E9D90DB1DAA9AA30272}

O TVSDK despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.

Os exemplos a seguir mostram a ordem de alguns eventos que ocorrem durante a reprodução.

Ao carregar com êxito um recurso de mídia por meio de `MediaPlayer.replaceCurrentResource`, a ordem dos eventos é:

1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Carregue o recurso de mídia no thread principal. Se você carregar um recurso de mídia em um thread em segundo plano, essa operação ou operações subsequentes poderão gerar um erro, como `MediaPlayerException`, e sair.

Ao preparar para reprodução por meio de `MediaPlayer.prepareToPlay`, a ordem dos eventos é:

1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` se anúncios foram inseridos.
1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.PREPARED`

Para fluxos ao vivo/lineares, durante a reprodução, à medida que a janela de reprodução avança e as oportunidades adicionais são resolvidas, a ordem dos eventos é:

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` se anúncios foram inseridos

## Ordem dos eventos de publicidade {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Quando a reprodução inclui publicidade, o TVSDK despacha eventos/notificações em sequências geralmente esperadas. O reprodutor pode implementar ações com base em eventos na sequência esperada.

Ao reproduzir anúncios, a ordem dos eventos é:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

Os seguintes eventos são despachados para cada anúncio no ad break:

* `MediaPlayerEvent.AD_BREAK_START`
* `MediaPlayerEvent.AD_START`
* `MediaPlayerEvent.AD_PROGRESS (multiple times)`
* `MediaPlayerEvent.AD_CLICK (for each click)`
* `MediaPlayerEvent.AD_COMPLETE`
* `MediaPlayerEvent.AD_BREAK_COMPLETE`

O exemplo a seguir mostra uma progressão típica dos eventos de reprodução de anúncio:

```
mediaPlayer.addEventListener(MediaPlayerEvent.AD_RESOLUTION_COMPLETE, new AdResolutionCompleteEventListener() { 
        @Override 
        public void onAdResolutionComplete() { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_START, new AdBreakStartedEventListener() { 
         @Override 
        public void onAdBreakStarted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_START, new AdStartedEventListener() { 
         @Override 
        public void onAdStarted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_PROGRESS, new AdProgressEventListener() { 
         @Override 
         public void onAdProgress(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_COMPLETE, new AdCompletedEventListener() { 
         @Override 
         public void onAdCompleted(AdPlaybackEvent adPlaybackEvent) { ... } 
    }); 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_BREAK_COMPLETE, new AdBreakCompletedEventListener() { 
         @Override 
         public void onAdBreakCompleted(AdBreakPlaybackEvent adBreakPlaybackEvent) { ... } 
    }); 
 
Below event is for tracking ad clicks. 
 
mediaPlayer.addEventListener(MediaPlayerEvent.AD_CLICK, new AdClickedEventListener() { 
         @Override 
         public void onAdClicked(AdClickEvent adClickEvent) { ... } 
    });
```

## Ordem dos eventos de DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas a DRM, como quando novos metadados de DRM são disponibilizados. O reprodutor pode implementar ações em resposta a esses eventos.

Para ser notificado sobre todos os eventos relacionados a DRM, escute `MediaPlayerEvent.DRM_METADATA`. O TVSDK despacha eventos de DRM adicionais por meio da classe `DRMManager` .

## Ordem dos eventos do carregador {#section_5638F8EDACCE422A9425187484D39DCC}

O TVSDK despacha `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` quando eventos de carregador ocorrem.