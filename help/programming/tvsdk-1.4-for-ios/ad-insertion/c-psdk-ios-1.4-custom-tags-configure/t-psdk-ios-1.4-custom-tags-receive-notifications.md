---
description: Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de notificação apropriado(s).
title: Adicionar ouvintes para notificações de metadados cronometrados
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 0%

---


# Adicionar ouvintes para notificações de metadados cronometrados {#add-listeners-for-timed-metadata-notifications}

Para receber notificações sobre tags no manifesto, implemente o(s) ouvinte(s) de notificação apropriado(s).

Você pode monitorar metadados cronometrados escutando os seguintes eventos, que notificam o aplicativo da atividade relacionada:

* `PTTimedMetadataChangedNotification`: Cada vez que uma tag assinada exclusiva é identificada durante a análise do conteúdo, o TVSDK prepara um novo  `PTTimedMetadata` objeto e despacha essa notificação.

   O objeto contém o nome da tag da qual você se inscreveu, o horário local na reprodução em que essa tag será exibida e outros dados.

* `PTMediaPlayerTimeChangeNotification` : Para fluxos ao vivo/lineares onde o manifesto/lista de reprodução é atualizado periodicamente, tags personalizadas adicionais podem aparecer na lista de reprodução/manifesto atualizado, portanto,  `TimedMetadata` objetos adicionais podem ser adicionados à  `MediaPlayerItem.timedMetadata` propriedade.

   Esse evento notifica seu aplicativo quando isso acontece.

   Recupere os metadados cronometrados de uma das seguintes maneiras.

   * Defina seu aplicativo para adicionar-se como um ouvinte à notificação `PTTimedMetadataChangedNotification` e busque o objeto usando `PTTimedMetadataKey`.

      ```
      [[NSNotificationCenter defaultCenter] addObserver:self selector:@selector(onTimedMetadataChanged:)  
        name:PTTimedMetadataChangedNotification object:self.player.currentItem]; 
      
      - (void) onTimedMetadataChanged:(NSNotification *) notification { 
          NSDictionary *timedMetadataUserInfo = [[NSDictionary alloc]initWithDictionary: notification.userInfo]; 
          PTTimedMetadata *newTimedMetadata = [timedMetadataUserInfo objectForKey: PTTimedMetadataKey]; 
      }
      ```

   * Acesse a propriedade `timedMetadataCollection` de `PTMediaPlayerItem`, que consiste em todos os objetos `PTTimedMetadata` que foram notificados até agora.

