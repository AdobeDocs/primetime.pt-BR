---
description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que apresentam problemas para fins de registro e depuração.
seo-description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que apresentam problemas para fins de registro e depuração.
seo-title: Classes de notificação
title: Classes de notificação
uuid: 3befc64b-4abd-47df-9c45-215b49029757
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 0%

---


# Classes de notificação {#notification-classes}

Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que apresentam problemas para fins de registro e depuração.

Pacote: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Nome da classe | Descrição |
|---|---|
| [Notificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | Classe que fornece mensagens informativas, avisos e erros. Encapsula a representação de objeto de um único evento de notificação em [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Retorna a descrição associada ao código de notificação fornecido e fornece constantes numéricas para objetos de notificação. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | Classe que armazena um log de objetos de notificação. Uma lista circular de [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) objetos que fornece acesso a uma lista de histórico de eventos de notificação. Ou seja, ele mantém uma lista de elementos, cada elemento contendo uma instância separada da classe [Notification](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html). |
| [NotificationHistoryItem](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | Classe que define uma entrada na lista circular em [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) e mantém a notificação e seu carimbo de data e hora. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | Classe que contém os tipos de notificações suportados. |

