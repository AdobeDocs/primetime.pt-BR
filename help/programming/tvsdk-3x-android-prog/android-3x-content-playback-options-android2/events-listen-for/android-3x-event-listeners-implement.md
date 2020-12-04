---
description: Os manipuladores de eventos permitem que você responda a eventos TVSDK.
seo-description: Os manipuladores de eventos permitem que você responda a eventos TVSDK.
seo-title: Implementação de ouvintes e retornos de chamada de evento
title: Implementação de ouvintes e retornos de chamada de evento
uuid: f186b39e-e634-4f64-977d-279147d76c5c
translation-type: tm+mt
source-git-commit: 1034a0520590777cc0930d2f732741202bc3bc04
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---


# Implementação de ouvintes e retornos de chamada de evento {#implement-event-listeners-and-callbacks}

Os manipuladores de eventos permitem que você responda a eventos TVSDK.

Quando um evento ocorre, o mecanismo de evento do TVSDK chama seu manipulador de eventos registrado, transmitindo as informações do evento.

O TVSDK define os ouvintes como interfaces internas públicas dentro da interface `MediaPlayer`.

Seu aplicativo deve implementar ouvintes de evento para qualquer evento TVSDK que afete seu aplicativo.

1. Determine que eventos seu aplicativo deve ouvir.

   * Eventos obrigatórios: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >Analise o evento de alteração de status, que ocorre quando o status do player muda de maneiras que você precisa saber. As informações fornecidas incluem erros que podem afetar o que seu player pode fazer em seguida.

   * Para outros eventos, dependendo do aplicativo, consulte [Resumo dos eventos do Primetime player](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

1. Implemente e adicione um ouvinte de evento para cada evento.

   Para a maioria dos eventos, o TVSDK envia argumentos para os ouvintes do evento. Esses valores fornecem informações sobre o evento que podem ajudá-lo a decidir o que fazer a seguir. A lista discriminada `MediaPlayerEvent` lista todos os eventos que `MediaPlayer` despacham. Para obter mais informações, consulte [Resumo dos eventos do player Primetime](../../android-3x-events-notifications/events-summary/android-3x-events-summary.md).

   Por exemplo, se `mPlayer` for uma instância de `MediaPlayer`, veja como você pode adicionar e estruturar um ouvinte de eventos:

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

O TVSDK despacha eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.

Os exemplos a seguir mostram a ordem de alguns eventos que ocorrem durante a reprodução.

Ao carregar com êxito um recurso de mídia por meio de `MediaPlayer.replaceCurrentResource`, a ordem dos eventos é:

1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.INITIALIZING`

1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.INITIALIZED`

>[!TIP]
>
>Carregue o recurso de mídia no thread principal. Se você carregar um recurso de mídia em um thread em segundo plano, essa operação ou operações subsequentes poderão gerar um erro, como `MediaPlayerException`, e sair.

Ao preparar a reprodução por `MediaPlayer.prepareToPlay`, a ordem dos eventos é:

1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.PREPARING`

1. `MediaPlayerEvent.TIMELINE_UPDATED` se as publicidades foram inseridas.
1. `MediaPlayerEvent.STATUS_CHANGED` com status  `MediaPlayerStatus.PREPARED`

Para fluxos ao vivo/lineares, durante a reprodução à medida que a janela de reprodução avança e oportunidades adicionais são resolvidas, a ordem dos eventos é:

1. `MediaPlayerEvent.ITEM_UPDATED`
1. `MediaPlayerEvent.TIMELINE_UPDATED` se anúncios foram inseridos

## Ordem dos eventos de publicidade {#section_7B3BE3BD3B6F4CF69D81F9CFAC24CAD5}

Quando a reprodução inclui publicidade, o TVSDK envia eventos/notificações em sequências geralmente esperadas. O player pode implementar ações com base em eventos na sequência esperada.

Ao reproduzir publicidades, a ordem dos eventos é:

* `MediaPlayerEvent.AD_RESOLUTION_COMPLETE`

Os seguintes eventos são enviados para cada anúncio dentro do intervalo do anúncio:

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

## Ordem dos eventos DRM {#section_3FECBF127B3E4EFEAB5AE87E89CCDE7C}

O TVSDK despacha eventos de gerenciamento de direitos digitais (DRM) em resposta a operações relacionadas ao DRM, como quando novos metadados do DRM ficam disponíveis. O player pode implementar ações em resposta a esses eventos.

Para ser notificado sobre todos os eventos relacionados ao DRM, aguarde `MediaPlayerEvent.DRM_METADATA`. O TVSDK despacha eventos DRM adicionais por meio da classe `DRMManager`.

## Ordem dos eventos do carregador {#section_5638F8EDACCE422A9425187484D39DCC}

O TVSDK despacha `MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE` quando eventos do carregador ocorrem.