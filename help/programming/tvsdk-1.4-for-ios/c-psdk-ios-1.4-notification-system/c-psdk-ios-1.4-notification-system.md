---
description: Os objetos de notificação PTN fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.
seo-description: Os objetos de notificação PTN fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.
seo-title: Notificações de status, atividade, erros e registros do player
title: Notificações de status, atividade, erros e registros do player
uuid: 59716a66-3736-4076-8011-8104bfe3a83a
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Notificações de status, atividade, erros e registro do player {#notifications-for-player-status-activity-errors-and-logs-overview}

Os objetos de notificação PTN fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.

Seu aplicativo pode recuperar as informações de notificação e status. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

>[!IMPORTANT]
>
>O TVSDK também usa *`notification`* para fazer referência a `NSNotifications` ( `PTMediaPlayer` notificações) *`event`* notificações, despachadas para fornecer informações sobre a atividade do player.

O TVSDK também emite problemas `PTMediaPlayerNewNotificationItemEntryNotification` ao emitir `PTNotification`.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem notificações `PTNotification` de status.

## Conteúdo da notificação {#notification-content}

O PTNotificação fornece informações relacionadas ao status do player.

O TVSDK fornece uma lista cronológica de `PTNotification` notificações. Cada notificação contém as seguintes informações:

* Carimbo de data e hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFO, AVISO ou ERRO.
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível pela pessoa da notificação, como SEEK_ERROR
   * `metadata`: Pares chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro `PTNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las para um servidor remoto para registro e representação gráfica.

## Configuração de notificação {#notification-setup}

O TVSDK configura o player para notificações básicas, embora você deva concluir a mesma configuração para suas notificações personalizadas.

Há duas implementações para `PTNotification`:

* Para ouvir
* Para adicionar notificações personalizadas a `PTNotificationHistory`

Para ouvir notificações, o TVSDK instancia a `PTNotification` classe e a anexa a uma instância do `PTMediaPlayerItem`, que está anexada a uma instância do PTMediaPlayer. Há apenas uma `PTNotificationHistory` instância por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Se você estiver adicionando personalizações, seus aplicativos e não o TVSDK, deverão executar essas etapas.

## Ouvir notificações {#listen-to-notifications}

Há duas maneiras de ouvir a `PTNotification` notificação no `PTMediaPlayer`:

1. Verifique manualmente a parte `PTNotificationHistory` do `PTMediaPlayerItem` formulário com um temporizador e verifique as diferenças:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Use a notificação [NSN](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) publicada do `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Registre-se no `NSNotification` usando a instância da `PTMediaPlayer` qual deseja obter notificações:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementar retornos de chamada de notificação {#implement-notification-callbacks}

Você pode implementar retornos de chamada de notificação.

1. Implemente o retorno de chamada de notificação obtendo as informações `PTNotification` do `NSNotification` usuário e lendo seus valores usando `PTMediaPlayerNotificationKey`:

   ```
   - (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
       PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
       NSLog(@"Notification: %@", notification); 
   }
   ```

## Adicionar notificações personalizadas {#add-custom-notifications}

Para adicionar uma notificação personalizada:
Crie um novo `PTNotification` e adicione-o ao `PTNotificationHistory` usando o `PTMediaPlayerItem`:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
