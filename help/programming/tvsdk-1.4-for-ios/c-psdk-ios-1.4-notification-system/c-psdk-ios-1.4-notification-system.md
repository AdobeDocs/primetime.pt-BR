---
description: Os objetos PTNotification fornecem informações sobre as alterações no status, nos avisos e nos erros do player. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.
title: Notificações para status, atividade, erros e logs do player
exl-id: 7f622c42-bc39-46e9-9b8b-4b3e467f37f7
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Notificações para status, atividade, erros e registro do player  {#notifications-for-player-status-activity-errors-and-logs-overview}

Os objetos PTNotification fornecem informações sobre as alterações no status, nos avisos e nos erros do player. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.

Seu aplicativo pode recuperar a notificação e as informações de status. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

>[!IMPORTANT]
>
>O TVSDK também usa *`notification`* para consultar `NSNotifications` ( `PTMediaPlayer` notificações) *`event`* notificações, enviadas para fornecer informações sobre a atividade do player.

O TVSDK também apresenta problemas `PTMediaPlayerNewNotificationItemEntryNotification` ao emitir `PTNotification`.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem `PTNotification` notificações de status.

## Conteúdo da notificação {#notification-content}

PTNotification fornece informações relacionadas ao status do reprodutor.

O TVSDK fornece uma lista cronológica de `PTNotification` notificações. Cada notificação contém as seguintes informações:

* Carimbo de data/hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFORMAÇÕES, AVISO ou ERRO.
   * `code`: uma representação numérica da notificação.
   * `name`: uma descrição legível da notificação, como SEEK_ERROR
   * `metadata`: Pares de chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` O fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outra `PTNotification` objeto que afeta diretamente esta notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las a um servidor remoto para registro e representação gráfica.

## Configuração de notificação {#notification-setup}

O TVSDK configura o reprodutor para notificações básicas, embora você deva concluir a mesma configuração para suas notificações personalizadas.

Há duas implementações para `PTNotification`:

* Para ouvir
* Para adicionar notificações personalizadas a `PTNotificationHistory`

Para ouvir notificações, o TVSDK instancia a variável `PTNotification` e a anexa a uma ocorrência de `PTMediaPlayerItem`, que é anexado a uma ocorrência de PTMediaPlayer. Há apenas um `PTNotificationHistory` instância por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Se você estiver adicionando personalizações, seus aplicativos, e não o TVSDK, deverão executar essas etapas.

## Ouvir notificações {#listen-to-notifications}

Há duas maneiras de ouvir `PTNotification` notificação na `PTMediaPlayer`:

1. Verifique manualmente o `PTNotificationHistory` do `PTMediaPlayerItem` com um temporizador e verifique as diferenças:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Usar o publicado [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) do `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Registre-se na `NSNotification` usando a instância do `PTMediaPlayer` a partir do qual você deseja obter notificações:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementar chamadas de retorno {#implement-notification-callbacks}

Você pode implementar chamadas de retorno de notificação.

1. Implemente o retorno de chamada de notificação obtendo o `PTNotification` do `NSNotification` informações do usuário e lendo seus valores usando `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## Adicionar notificações personalizadas {#add-custom-notifications}

Para adicionar uma notificação personalizada: Crie uma nova `PTNotification` e adicione-o à `PTNotificationHistory` usando o atual `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
