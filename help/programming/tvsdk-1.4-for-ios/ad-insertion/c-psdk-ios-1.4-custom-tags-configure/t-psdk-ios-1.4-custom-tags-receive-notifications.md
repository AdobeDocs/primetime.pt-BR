---
description: Para receber notificações sobre tags no manifesto, implemente os ouvintes de notificação apropriados.
seo-description: Para receber notificações sobre tags no manifesto, implemente os ouvintes de notificação apropriados.
seo-title: Adicionar ouvintes para notificações de metadados cronometrados
title: Adicionar ouvintes para notificações de metadados cronometrados
uuid: dcd1bd92-0617-4eab-8b06-7301aaff42f3
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 0%

---


# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, implemente os ouvintes de notificação apropriados.

Você pode monitorar os metadados cronometrados ouvindo os seguintes eventos, que notificam sua aplicação da atividade relacionada:

* `PTTimedMetadataChangedNotification`: Cada vez que uma tag assinada exclusiva é identificada durante a análise do conteúdo, o TVSDK prepara um novo  `PTTimedMetadata` objeto e despacha essa notificação.

   O objeto contém o nome da tag na qual você se inscreveu, a hora local na reprodução em que essa tag será exibida e outros dados.

* `PTMediaPlayerTimeChangeNotification` : Para fluxos ao vivo/lineares nos quais o manifesto/lista de reprodução é atualizado periodicamente, outras tags personalizadas podem aparecer na lista de reprodução/manifesto atualizado, portanto,  `TimedMetadata` objetos adicionais podem ser adicionados à  `MediaPlayerItem.timedMetadata` propriedade.

   Este evento notifica seu aplicativo quando isso acontece.

   Recupere os metadados cronometrados de uma das seguintes maneiras.

   * Configure seu aplicativo para adicionar-se como um ouvinte à notificação `PTTimedMetadataChangedNotification` e busque o objeto usando `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Acesse a propriedade `timedMetadataCollection` de `PTMediaPlayerItem`, que consiste em todos os objetos `PTTimedMetadata` que foram notificados até o momento.

