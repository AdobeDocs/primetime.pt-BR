---
description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.
seo-description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.
seo-title: Classes de notificação
title: Classes de notificação
uuid: 8a276056-775f-432d-a4b4-722f6e4e278f
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# Classes de notificação {#notification-classes}

Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.

| **Nome da classe** | **Descrição** |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Classe que descreve a notificação de um erro que faz com que o player pare a reprodução. Esta é uma notificação [PTNotificação](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) do tipo de notificação ERROR. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Lista todas as notificações enviadas pela estrutura do Primetime Player. |
| [Notificação PTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Classe que fornece mensagens informativas, avisos e erros. Encapsula a representação de objeto de um único evento de notificação em [PTNotifiedHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [PTNotificaçãoHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Classe que armazena um log de objetos de notificação [PTNotifiedHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) objetos que fornecem acesso a uma lista de histórico de eventos de notificação. Ou seja, ele mantém uma lista de elementos, cada elemento contendo uma instância separada da notificação [PTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [PTNotifiedHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Classe que define uma entrada na lista circular em [PTNotifiedHistory](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) e mantém a notificação e seu carimbo de data e hora. |

