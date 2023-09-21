---
description: Os eventos do TVSDK indicam o estado do reprodutor, os erros que ocorrem, a conclusão das ações solicitadas, como o início da reprodução de um vídeo ou as ações que ocorrem implicitamente, como a conclusão de um anúncio.
title: Analise eventos do Primetime Player
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '236'
ht-degree: 0%

---

# Visão geral {#implement-event-listeners-and-callbacks-overview}

Os manipuladores de eventos permitem que o TVSDK responda aos eventos. Quando um evento ocorre, o mecanismo de eventos do TVSDK chama o manipulador de eventos registrado e transmite as informações do evento para o manipulador.

O Tempo de execução do Flash fornece um mecanismo de eventos genérico, que o TVSDK também usa e define uma série de eventos personalizados. Seu aplicativo deve implementar ouvintes de eventos para eventos TVSDK que afetam seu aplicativo.

1. Determine para quais eventos seu aplicativo deve ouvir.

   * **Eventos obrigatórios**: Analise todos os eventos de reprodução.

     >[!IMPORTANT]
     >
     >O evento de reprodução `MediaPlayerStatusChangeEvent.STATUS_CHANGE` fornece o status do reprodutor, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do player.

   * **Outros eventos**: opcional, dependendo do aplicativo.

     Por exemplo, se você incorporar anúncios na reprodução, ouça todos os `AdBreakPlaybackEvent` e `AdPlaybackEvent` eventos.

1. Implemente ouvintes de eventos para cada evento.

   O TVSDK retorna valores de parâmetro para os retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar nos ouvintes para executar as ações apropriadas.

   A variável `Event` A classe lista todas as interfaces de retorno de chamada. Cada interface exibe os parâmetros retornados para ela.

   Por exemplo:

   ```
   public function MediaPlayerStatusChangeEvent(type:String,  
                   bubbles:Boolean = false,  
                   cancelable:Boolean = false,  
                   status:String = null,  
                   error:MediaError = null) 
   ```

1. Registre seus ouvintes de retorno de chamada com o `MediaPlayer` objeto usando `MediaPlayer.addEventListener`.

   `MediaPlayer` estende `flash.events.IEventDispatcher`, que faz parte dos arquivos principais do reprodutor do Flash e inclui as funções `addEventListener` e `removeEventListener`.

   ```
   mediaPlayer.addEventListener( 
     MediaPlayerStatusChangeEvent.STATUS_CHANGED,  
     onStatusChanged);
   ```
