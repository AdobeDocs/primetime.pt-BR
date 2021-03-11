---
description: Os eventos do TVSDK indicam o estado do reprodutor, os erros que ocorrem, a conclusão de ações solicitadas, como o início da reprodução de um vídeo ou ações que ocorrem implicitamente, como a conclusão de um anúncio.
title: Analise os eventos do Player do Primetime
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---


# Visão geral {#implement-event-listeners-and-callbacks-overview}

Os manipuladores de eventos permitem que o TVSDK responda aos eventos. Quando um evento ocorre, o mecanismo de evento do TVSDK chama o manipulador de eventos registrado e transmite as informações do evento para o manipulador.

O Flash Runtime fornece um mecanismo de eventos genéricos, que o TVSDK também usa e define uma série de eventos personalizados. Seu aplicativo deve implementar ouvintes de eventos para eventos TVSDK que afetam seu aplicativo.

Para obter uma lista completa dos eventos da análise de vídeo, consulte [Rastrear reprodução de vídeo principal](https://marketing.adobe.com/resources/help/en_US/sc/appmeasurement/hbvideo/c_vhl_track-core-vid-playback.html).

1. Determine quais eventos seu aplicativo deve ouvir.

   * **Eventos** obrigatórios: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >O evento de reprodução `MediaPlayerStatusChangeEvent.STATUS_CHANGE` fornece o status do reprodutor, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do player.

   * **Outros eventos**: Opcional, dependendo do seu aplicativo.

      Por exemplo, se você incorporar publicidade em sua reprodução, analise todos os eventos `AdBreakPlaybackEvent` e `AdPlaybackEvent`.

1. Implemente ouvintes de eventos para cada evento.

   O TVSDK retorna valores de parâmetro para seus retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar em seus ouvintes para executar as ações apropriadas.

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

   `MediaPlayer` O estende  `flash.events.IEventDispatcher`, que faz parte dos arquivos principais do reprodutor do Flash e inclui as funções  `addEventListener` e  `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```


