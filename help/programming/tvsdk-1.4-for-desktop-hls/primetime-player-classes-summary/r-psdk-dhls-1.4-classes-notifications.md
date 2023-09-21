---
description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que geram problemas para fins de log e depuração.
title: Classes de notificação
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '280'
ht-degree: 0%

---

# Classes de notificação {#notification-classes}

Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que geram problemas para fins de log e depuração.

Pacote: [com.adobe.mediacore.notifications](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/package-detail.html)

| Nome da classe | Descrição |
|---|---|
| [Notificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) | Classe que fornece mensagens informativas, avisos e erros. Encapsula a representação do objeto de um único evento de notificação em [HistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html). |
| [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationCode.html) | Retorna a descrição associada ao código de notificação fornecido e fornece constantes numéricas para objetos de notificação. |
| [HistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) | Classe que armazena um log de objetos de notificação. Uma lista circular de [ItemHistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) objetos que fornecem acesso a uma lista de histórico de eventos de notificação. Ou seja, mantém uma lista de elementos, cada elemento contendo uma instância separada do [Notificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/Notification.html) classe. |
| [ItemHistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistoryItem.html) | Classe que define uma entrada na lista circular em [HistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationHistory.html) e mantém a notificação e seu carimbo de data e hora. |
| [NotificationType](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/notifications/NotificationType.html) | Classe que contém os tipos de notificações aceitos. |
