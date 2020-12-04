---
description: A parte de notificação da biblioteca TVSDK do navegador permite criar um sistema de log e depuração que pode ser útil para fins de diagnóstico e validação.
seo-description: A parte de notificação da biblioteca TVSDK do navegador permite criar um sistema de log e depuração que pode ser útil para fins de diagnóstico e validação.
seo-title: Sistema de notificação
title: Sistema de notificação
uuid: 69c4ff1d-3167-413b-ab49-942a5ddc34d7
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Sistema de notificação {#notification-system}

A parte de notificação da biblioteca TVSDK do navegador permite criar um sistema de log e depuração que pode ser útil para fins de diagnóstico e validação.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

O TVSDK do navegador tem uma política *no throp* para sua API. A maioria dos métodos retorna um valor `PSDKErrorCode` para indicar se o método foi executado com êxito. Para obter uma lista completa de todos os valores possíveis de `PSDKErrorCode`, consulte Referências da API TVSDK do navegador.

Erros assíncronos são notificados por meio dos eventos específicos.

O TVSDK do navegador envia eventos `MediaPlayer` para fornecer informações sobre a atividade do player. Você deve implementar ouvintes de evento para capturar e responder a esses eventos.

>[!TIP]
>
>Eventos principais e informações são registradas no console do navegador da Web.

## Escutar notificações {#section_06B96633433D497E842FB7ADD5F2C7DA}

Você pode ouvir notificações e adicionar suas próprias notificações ao histórico de notificações. O núcleo do sistema de notificação TVSDK do navegador é a classe `Notification`, que representa uma notificação independente.

Para configurar seu aplicativo para escutar notificações:

1. Analise as alterações de status do MediaPlayer usando a instância do MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente o retorno de chamada.

   O retorno de chamada recebe uma instância do `AdobePSDK.MediaPlayerStatusChangeEvent`, e o TVSDK do navegador transmite esse objeto de evento para o retorno de chamada que contém o novo estado do player.
1. Seu aplicativo pode ouvir outros eventos que são despachados pelo TVSDK do navegador usando a instância `MediaPlayer`.

