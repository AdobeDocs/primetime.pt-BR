---
description: Eventos do TVSDK indicam o estado do player, os erros que ocorrem, a conclusão de ações solicitadas, como o início da reprodução de um vídeo ou ações que ocorrem implicitamente, como a conclusão de um anúncio.
seo-description: Eventos do TVSDK indicam o estado do player, os erros que ocorrem, a conclusão de ações solicitadas, como o início da reprodução de um vídeo ou ações que ocorrem implicitamente, como a conclusão de um anúncio.
seo-title: Ouça eventos do Primetime Player
title: Ouça eventos do Primetime Player
uuid: e72782bf-9d26-4285-85e4-fd4d803c1bbe
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 0%

---


# Visão geral {#implement-event-listeners-and-callbacks-overview}

Os manipuladores de eventos permitem que o TVSDK responda aos eventos. Quando um evento ocorre, o mecanismo de evento do TVSDK chama o manipulador de eventos registrado e transmite as informações do evento ao manipulador.

O Flash Runtime fornece um mecanismo de eventos genéricos, que o TVSDK também usa e define uma série de eventos personalizados. Seu aplicativo deve implementar ouvintes de evento para eventos TVSDK que afetam seu aplicativo.

Para obter uma lista completa dos eventos para análise de vídeo, consulte [Rastrear reprodução de vídeo principal](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html).

1. Determine para quais eventos seu aplicativo deve ouvir.

   * **Eventos** obrigatórios: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >O evento de reprodução `MediaPlayerStatusChangeEvent.STATUS_CHANGE` fornece o status do player, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do seu player.

   * **Outros eventos**: Opcional, dependendo do aplicativo.

      Por exemplo, se você incorporar publicidade na reprodução, ouça todos os eventos `AdBreakPlaybackEvent` e `AdPlaybackEvent`.

1. Implemente ouvintes de evento para cada evento.

   O TVSDK retorna valores de parâmetro para os retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar em seus ouvintes para executar ações apropriadas.

   A classe `Event` lista todas as interfaces de retorno de chamada. Cada interface exibe os parâmetros retornados para essa interface.

   Por exemplo:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registre seus ouvintes de retorno de chamada com o objeto `MediaPlayer` usando `MediaPlayer.addEventListener`.

   `MediaPlayer` estende  `flash.events.IEventDispatcher`, que faz parte dos arquivos principais do player do Flash e inclui as funções  `addEventListener` e  `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


