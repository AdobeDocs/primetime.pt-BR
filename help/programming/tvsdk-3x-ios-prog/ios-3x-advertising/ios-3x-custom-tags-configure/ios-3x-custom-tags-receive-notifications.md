---
description: Para receber notificações sobre tags no manifesto, implemente os ouvintes de notificação apropriados.
seo-description: Para receber notificações sobre tags no manifesto, implemente os ouvintes de notificação apropriados.
seo-title: Adicionar ouvintes para notificações de metadados cronometrados
title: Adicionar ouvintes para notificações de metadados cronometrados
uuid: b6939011-a6ff-4342-8e7c-3a0c805ee91c
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, implemente os ouvintes de notificação apropriados.

Você pode monitorar os metadados cronometrados ao acompanhar os seguintes eventos, que notificam sua aplicação da atividade relacionada:

* `PTTimedMetadataChangedNotification`: Cada vez que uma tag assinada exclusiva é identificada durante a análise do conteúdo, o TVSDK prepara um novo `PTTimedMetadata` objeto e despacha essa notificação.

   O objeto contém o nome da tag na qual você se inscreveu, a hora local na reprodução em que essa tag será exibida e outros dados.

* `PTMediaPlayerTimeChangeNotification` : Para fluxos ao vivo/lineares nos quais o manifesto/lista de reprodução é atualizado periodicamente, outras tags personalizadas podem aparecer na lista de reprodução/manifesto atualizado, de modo que `TimedMetadata` objetos adicionais podem ser adicionados à `MediaPlayerItem.timedMetadata` propriedade.

   Este evento notifica seu aplicativo quando isso acontece.

   Recupere os metadados cronometrados de uma das seguintes maneiras.

   * Configure seu aplicativo para adicionar-se como um ouvinte à `PTTimedMetadataChangedNotification` notificação e busque o objeto usando `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Acesse a `timedMetadataCollection` propriedade de `PTMediaPlayerItem`, que consiste em todos os `PTTimedMetadata` objetos que foram notificados até o momento.