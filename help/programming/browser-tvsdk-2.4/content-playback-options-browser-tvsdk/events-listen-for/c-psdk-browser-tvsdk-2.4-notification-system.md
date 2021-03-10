---
description: A parte de notificação da biblioteca TVSDK do navegador permite criar um sistema de log e depuração que pode ser útil para fins de diagnóstico e validação.
title: Sistema de notificação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---


# Sistema de notificação {#notification-system}

A parte de notificação da biblioteca TVSDK do navegador permite criar um sistema de log e depuração que pode ser útil para fins de diagnóstico e validação.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

O TVSDK do navegador tem uma política *no launch* para sua API. A maioria dos métodos retorna um valor `PSDKErrorCode` para indicar se o método foi executado com êxito. Para obter uma lista completa de todos os valores possíveis `PSDKErrorCode`, consulte Referências da API do TVSDK do navegador.

Erros assíncronos são notificados por meio de eventos específicos.

O TVSDK do navegador despacha eventos `MediaPlayer` para fornecer informações sobre a atividade do reprodutor. Você deve implementar ouvintes de eventos para capturar e responder a esses eventos.

>[!TIP]
>
>Os principais eventos e informações são registrados no console do navegador da Web.

## Analise as notificações {#section_06B96633433D497E842FB7ADD5F2C7DA}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações. O núcleo do sistema de notificação TVSDK do navegador é a classe `Notification` , que representa uma notificação independente.

Para configurar seu aplicativo para ouvir notificações:

1. Analise as alterações de status do MediaPlayer usando a instância do MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente o retorno de chamada.

   O retorno de chamada recebe uma instância do `AdobePSDK.MediaPlayerStatusChangeEvent` e o TVSDK do Navegador transmite esse objeto de evento para o retorno de chamada que contém o novo estado do player.
1. Seu aplicativo pode ouvir outros eventos despachados pelo Browser TVSDK usando a instância `MediaPlayer`.

