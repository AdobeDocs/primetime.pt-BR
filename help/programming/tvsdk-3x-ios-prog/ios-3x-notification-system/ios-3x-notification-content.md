---
description: Os objetos de notificação PTN fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.
seo-description: Os objetos de notificação PTN fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.
seo-title: Conteúdo da notificação
title: Conteúdo da notificação
uuid: d42d2e89-1bdd-4be0-8a69-821fec6bbc75
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 0%

---


# Notificações de status, atividade, erros e registro do player {#notifications-player-status-activity-errors-logging}

`PTNotification` objetos fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.

Seu aplicativo pode recuperar as informações de notificação e status. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

>[!NOTE]
>
>O TVSDK também usa *`notification`* para se referir a `NSNotifications` ( `PTMediaPlayer` notificações) *`event`* notificações, despachadas para fornecer informações sobre a atividade do player.

O TVSDK também emite `PTMediaPlayerNewNotificationItemEntryNotification` quando emite `PTNotification`.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem notificações de status `PTNotification`.

## Conteúdo de notificação {#notification-content}

`PTNotification` fornece informações relacionadas ao status do player.

O TVSDK fornece uma lista cronológica de `PTNotification` notificações. Cada notificação contém as seguintes informações:

* Carimbo de data e hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * `type`: INFO, AVISO ou ERRO.
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível pela pessoa da notificação, como SEEK_ERROR
   * `metadata`: Pares chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro  `PTNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las para um servidor remoto para registro e representação gráfica.

## Configuração de notificação {#notification-setup}

O TVSDK configura o player para notificações básicas, embora você deva concluir a mesma configuração para suas notificações personalizadas.

Há duas implementações para `PTNotification`:

* Para ouvir
* Para adicionar notificações personalizadas a `PTNotificationHistory`

Para ouvir notificações, o TVSDK instancia a classe `PTNotification` e a anexa a uma instância do `PTMediaPlayerItem`, que está anexada a uma instância do PTMediaPlayer. Há apenas uma instância `PTNotificationHistory` por `PTMediaPlayer`.

>[!IMPORTANT]
>
>Se você estiver adicionando personalizações, seus aplicativos e não o TVSDK, deverão executar essas etapas.

## Escutar notificações {#listen-to-notifications}

Há duas maneiras de ouvir a notificação `PTNotification` em `PTMediaPlayer`:

1. Verifique manualmente `PTNotificationHistory` do `PTMediaPlayerItem` com um temporizador e verifique as diferenças:

   ```
   //Access to the PTMediaPlayerItem  
   PTMediaPlayerItem *item = self.player.currentItem; 
   PTNotificationHistory *notificationHistory = item.notificationHistory; 
   
   //Get the list of notification events from the notification History  
   NSArray *notifications = notificationHistory.notificationItems;
   ```

1. Use o [NSNotificação](https://developer.apple.com/library/mac/%23documentation/Cocoa/Reference/Foundation/Classes/NSNotification_Class/Reference/Reference.html) publicado de `PTMediaPlayerPTMediaPlayerNewNotificationEntryAddedNotification`.
1. Registre-se em `NSNotification` usando a instância de `PTMediaPlayer` da qual deseja obter notificações:

   ```
   //Register to the NSNotification 
   
   [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onMediaPlayerNotification:)  
     name:PTMediaPlayerNewNotificationEntryAddedNotification object:self.player];
   ```

## Implementar retornos de chamada de notificação {#implement-notification-callbacks}

Você pode implementar retornos de chamada de notificação.

Implemente o retorno de chamada de notificação obtendo `PTNotification` das `NSNotification` informações do usuário e lendo seus valores usando `PTMediaPlayerNotificationKey`:

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
