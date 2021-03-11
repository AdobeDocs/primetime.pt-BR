---
description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.
title: Classes de notificação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---


# Classes de notificação{#notification-classes}

Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.

| Nome da classe | Descrição |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Classe que descreve a notificação de um erro que faz com que o reprodutor pare a reprodução. Este é um [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) do tipo de notificação ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Lista todas as notificações enviadas pela estrutura do Primetime Player. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Classe que fornece mensagens informativas, avisos e erros. Encapsula a representação de objeto de um único evento de notificação em [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Classe que armazena um log de objetos de notificação [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) objetos que fornecem acesso a uma lista de histórico de eventos de notificação. Ou seja, ele mantém uma lista de elementos, cada elemento contendo uma instância separada de [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Classe que define uma entrada na lista circular em [PTNotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) e contém a notificação e seu carimbo de data e hora. |

