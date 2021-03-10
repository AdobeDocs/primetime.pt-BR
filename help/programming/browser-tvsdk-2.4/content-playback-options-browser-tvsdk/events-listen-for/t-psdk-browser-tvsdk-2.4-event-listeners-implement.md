---
description: Os manipuladores de eventos permitem que o Browser TVSDK responda aos eventos.
title: Implementar ouvintes e retornos de chamada do evento
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 1%

---


# Implementar ouvintes de eventos e retornos de chamada{#implement-event-listeners-and-callbacks}

Os manipuladores de eventos permitem que o Browser TVSDK responda aos eventos.

Quando um evento ocorre, o mecanismo de evento do TVSDK do navegador chama o manipulador de eventos registrado e transmite as informações do evento para o manipulador.

Seu aplicativo deve implementar ouvintes de eventos para eventos TVSDK do navegador que afetam seu aplicativo.

1. Determine quais eventos seu aplicativo deve ouvir.

   * **Eventos** obrigatórios: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >O evento de reprodução `STATUS_CHANGED` fornece o estado do player, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do player.

   * **Outros eventos**: Opcional, dependendo do seu aplicativo.

      Por exemplo, se você incorporar publicidade em sua reprodução, analise todos os eventos `AdBreakPlaybackEvent` e `AdPlaybackEvent`.

1. Implemente ouvintes de eventos para cada evento.

   O TVSDK do navegador retorna valores de parâmetro para seus retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar em seus ouvintes para executar as ações apropriadas.

   Por exemplo:

   * Tipo de evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Propriedade do evento: `MediaPlayerStatus.<event>` usado desta forma:

```js
player.addEventListener( 
            AdobePSDK.PSDKEventType.STATUS_CHANGED,  
            onStatusChange); 
 
onStatusChange = function (event) { 
 
    switch (event.status) { 
        case AdobePSDK.MediaPlayerStatus.IDLE: 
            console.log("Player Status: IDLE"); 
            break;
```

1. Registre seus ouvintes de retorno de chamada com o objeto `MediaPlayer` usando `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
