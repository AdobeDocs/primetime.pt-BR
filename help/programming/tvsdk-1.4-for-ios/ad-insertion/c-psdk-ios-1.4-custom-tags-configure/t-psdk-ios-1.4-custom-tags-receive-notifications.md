---
description: Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de notificação apropriado(s).
title: Adicionar ouvintes para notificações de metadados cronometrados
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---

# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de notificação apropriado(s).

Você pode monitorar metadados cronometrados ouvindo os seguintes eventos, que notificam seu aplicativo sobre atividades relacionadas:

* `PTTimedMetadataChangedNotification`: Cada vez que uma tag única assinada é identificada durante a análise do conteúdo, o TVSDK prepara uma nova `PTTimedMetadata` e envia esta notificação.

  O objeto contém o nome da tag que você assinou, o horário local na reprodução em que essa tag aparecerá e outros dados.

* `PTMediaPlayerTimeChangeNotification` : Para fluxos ao vivo/lineares nos quais o manifesto/lista de reprodução é atualizado periodicamente, tags personalizadas adicionais podem aparecer na lista de reprodução/manifesto atualizada, portanto, tags adicionais `TimedMetadata` objetos podem ser adicionados à `MediaPlayerItem.timedMetadata` propriedade.

  Esse evento notifica seu aplicativo quando isso ocorre.

  Recupere os metadados cronometrados de uma das seguintes maneiras.

   * Defina seu aplicativo para se adicionar como um ouvinte à variável `PTTimedMetadataChangedNotification` notificação e buscar o objeto usando `PTTimedMetadataKey`.

     ```
     [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
       name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
     
     - (void) onTimedMetadataChanged:(NSNotification *) notification { 
         NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
         PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
     }
     ```

   * Acesse o `timedMetadataCollection` propriedade de `PTMediaPlayerItem`, que consiste em todos os `PTTimedMetadata` objetos que foram notificados até o momento.
