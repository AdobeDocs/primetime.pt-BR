---
description: Os manipuladores de eventos permitem que o navegador TVSDK responda aos eventos.
title: Implementar ouvintes e retornos de chamada de evento
exl-id: 2ab33c03-4df6-48e5-825c-95aeef8855d2
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 0%

---

# Implementar ouvintes e retornos de chamada de evento{#implement-event-listeners-and-callbacks}

Os manipuladores de eventos permitem que o navegador TVSDK responda aos eventos.

Quando um evento ocorre, o mecanismo de evento do TVSDK do navegador chama o manipulador de eventos registrado e transmite as informações do evento para o manipulador.

Seu aplicativo deve implementar ouvintes de eventos para eventos TVSDK do navegador que afetam seu aplicativo.

1. Determine para quais eventos seu aplicativo deve ouvir.

   * **Eventos obrigatórios**: Analise todos os eventos de reprodução.

      >[!IMPORTANT]
      >
      >O evento de reprodução `STATUS_CHANGED` O fornece o estado do player, incluindo erros. Qualquer um dos estados pode afetar a próxima etapa do player.

   * **Outros eventos**: opcional, dependendo do aplicativo.

      Por exemplo, se você incorporar anúncios na reprodução, ouça todos os `AdBreakPlaybackEvent` e `AdPlaybackEvent` eventos.

1. Implemente ouvintes de eventos para cada evento.

   O TVSDK do navegador retorna valores de parâmetro para seus retornos de chamada do ouvinte de eventos. Esses valores fornecem informações relevantes sobre o evento que você pode usar nos ouvintes para executar as ações apropriadas.

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
