---
description: Os manipuladores de eventos permitem que o TVSDK do navegador responda aos eventos.
seo-description: Os manipuladores de eventos permitem que o TVSDK do navegador responda aos eventos.
seo-title: Implementar ouvintes e retornos de chamada de evento
title: Implementar ouvintes e retornos de chamada de evento
uuid: 63f62c60-505e-4f83-bc0d-58895d85a75a
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed

---


# Implementar ouvintes e retornos de chamada de evento{#implement-event-listeners-and-callbacks}

Os manipuladores de eventos permitem que o TVSDK do navegador responda aos eventos.

Quando um evento ocorre, o mecanismo de evento do TVSDK do navegador chama seu manipulador de eventos registrado e transmite as informações do evento ao manipulador.

Seu aplicativo deve implementar ouvintes de eventos para eventos TVSDK do navegador que afetam seu aplicativo.

1. Determine para quais eventos seu aplicativo deve ouvir.

   * **Eventos** obrigatórios: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >O evento reproduzir `STATUS_CHANGED` fornece o estado do player, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do seu player.

   * **Outros eventos**: Opcional, dependendo do aplicativo.

      Por exemplo, se você incorporar publicidade na reprodução, ouça todos os `AdBreakPlaybackEvent` eventos e `AdPlaybackEvent` eventos.

1. Implemente ouvintes de eventos para cada evento.

   O TVSDK do navegador retorna valores de parâmetro para os retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar em seus ouvintes para executar ações apropriadas.

   Por exemplo:

   * Tipo de evento: `AdobePSDK.PSDKEventType.STATUS_CHANGED`
   * Propriedade do evento: `MediaPlayerStatus.<event>` usado assim:

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

1. Registre seus ouvintes de retorno de chamada com o `MediaPlayer` objeto usando `MediaPlayer.addEventListener`.

   ```js
   player.addEventListener(AdobePSDK.PSDKEventType.STATUS_CHANGED,  
                                    onStatusChange);
   ```
