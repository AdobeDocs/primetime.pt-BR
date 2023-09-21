---
description: A parte de notificação da biblioteca TVSDK do navegador permite criar um sistema de log e depuração que pode ser útil para fins de diagnóstico e validação.
title: Sistema de notificação
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 0%

---

# Sistema de notificação {#notification-system}

A parte de notificação da biblioteca TVSDK do navegador permite criar um sistema de log e depuração que pode ser útil para fins de diagnóstico e validação.

<!--<a id="section_EC5DBE8DDA434B70A01FA2F3EF4618BD"></a>-->

O TVSDK do navegador tem um *sem lançamento* para sua API. A maioria dos métodos retorna um `PSDKErrorCode` valor para indicar se o método foi executado com êxito. Para obter uma lista completa de todos os possíveis `PSDKErrorCode` valores, consulte Referências da API TVSDK do navegador.

Os erros assíncronos são notificados por meio dos eventos específicos.

Despachos TVSDK do navegador `MediaPlayer` eventos para fornecer informações sobre a atividade do player. Você deve implementar ouvintes de eventos para capturar e responder a esses eventos.

>[!TIP]
>
>Os eventos e as informações principais são registrados no console do navegador da Web.

## Acompanhar notificações {#section_06B96633433D497E842FB7ADD5F2C7DA}

Você pode ouvir notificações e adicionar suas próprias notificações ao histórico de notificações. O núcleo do sistema de notificação do TVSDK do navegador é o `Notification` classe, que representa uma notificação independente.

Para configurar sua aplicação para acompanhar notificações:

1. Analise as alterações de status do MediaPlayer usando a instância MediaPlayer.

   ```js
   player.addEventListener( 
         AdobePSDK.PSDKEventType.STATUS_CHANGED, onStatusChange);
   ```

1. Implemente o retorno de chamada.

   O retorno de chamada recebe uma instância do `AdobePSDK.MediaPlayerStatusChangeEvent`, e o TVSDK do navegador passa esse objeto de evento para o retorno de chamada que contém o novo estado do player.
1. Seu aplicativo pode ouvir outros eventos despachados pelo TVSDK do navegador usando o `MediaPlayer` instância.
