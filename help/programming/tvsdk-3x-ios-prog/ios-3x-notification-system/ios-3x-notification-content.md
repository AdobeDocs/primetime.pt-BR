---
description: Os objetos PTNotification fornecem informações sobre alterações no status do player, avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.
title: Conteúdo de notificação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 0%

---


# Notificações para status do player, atividade, erros e registro {#notifications-player-status-activity-errors-logging}

`PTNotification` objetos fornecem informações sobre alterações no status do player, avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.

Seu aplicativo pode recuperar a notificação e as informações de status. Você também pode criar um sistema de registro para diagnósticos e validação usando as informações de notificação.

>[!NOTE]
>
>O TVSDK também usa *`notification`* para se referir a `NSNotifications` ( `PTMediaPlayer` notificações) *`event`* notificações, despachadas para fornecer informações sobre a atividade do reprodutor.

O TVSDK também emite `PTMediaPlayerNewNotificationItemEntryNotification` quando emite `PTNotification`.

Você implementa ouvintes de eventos para capturar e responder aos eventos. Muitos eventos fornecem notificações de status `PTNotification`.

## Conteúdo de notificação {#notification-content}

`PTNotification` fornece informações relacionadas ao status do reprodutor.

O TVSDK fornece uma lista cronológica de notificações `PTNotification`. Cada notificação contém as seguintes informações:

* Carimbo de data/hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFO, AVISO ou ERRO.
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível da notificação, como SEEK_ERROR
   * `metadata`: Pares de chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro  `PTNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las a um servidor remoto para registro e representação gráfica.

## Configuração de notificação {#notification-setup}

O TVSDK configura o reprodutor para notificações básicas, embora você deva concluir a mesma configuração para suas notificações personalizadas.

Há duas implementações para `PTNotification`:

* Para ouvir
* Para adicionar notificações personalizadas a `PTNotificationHistory`

Para ouvir notificações, o TVSDK instancia a classe `PTNotification` e a anexa a uma instância do `PTMediaPlayerItem`, que é anexada a uma instância PTMediaPlayer. Há apenas uma instância `PTNotificationHistory` por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Se você estiver adicionando personalizações, seus aplicativos e não o TVSDK, deverão executar essas etapas.

## Ouça as notificações {#listen-to-notifications}

Há duas maneiras de ouvir a notificação `PTNotification` no `PTMediaPlayer`:

1. Verifique manualmente o `PTNotificationHistory` do `PTMediaPlayerItem` com um temporizador e verifique as diferenças:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Use o [NSNotification](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) postado do `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Registre-se no `NSNotification` usando a instância do `PTMediaPlayer` do qual deseja obter notificações:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementar retornos de chamada de notificação {#implement-notification-callbacks}

É possível implementar retornos de chamada de notificação.

Implemente o retorno de chamada de notificação obtendo o `PTNotification` das informações do usuário `NSNotification` e lendo seus valores usando `PTMediaPlayerNotificationKey`:

```
- (void) onMediaPlayerNotification:(NSNotification *) nsnotification { 
    PTNotification *notification = [nsnotification.userInfo objectForKey:PTMediaPlayerNotificationKey]; 
    NSLog(@"Notification: %@", notification); 
}
```

## Adicionar notificações personalizadas {#add-custom-notifications}

Para adicionar uma notificação personalizada:
Crie um novo `PTNotification` e adicione-o ao `PTNotificationHistory` usando o `PTMediaPlayerItem` atual:

```
//Access to the PTMediaPlayerItem  
PTMediaPlayerItem *item = self.player.currentItem; 
PTNotificationHistory *notificationHistory = item.notificationHistory; 
 
//Create notification 
PTNotification* notification = [[PTNotification notificationWithType:PTNotificationTypeWarning code:99999 description:@"Custom notification description"]; 
 
//Add notification 
[notificationHistory addNotification:notification];
```
