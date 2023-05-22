---
description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.
title: Classes de notificação
exl-id: 611a886b-a77a-4092-ab05-25e496fec8b1
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Classes de notificação{#notification-classes}

Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.

| Nome da classe | Descrição |
|---|---|
| [PTMediaError](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaError.html) | Classe que descreve a notificação para um erro que faz com que o reprodutor pare de ser reproduzido. Este é um [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) do tipo de notificação ERRO. |
| [PTMediaPlayerNotifications](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerNotifications.html) | Lista todas as notificações expedidas pela estrutura do Primetime Player. |
| [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) | Classe que fornece mensagens informativas, avisos e erros. Encapsula a representação do objeto de um único evento de notificação em [HistóricoDeNotificaçãoPTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html). |
| [HistóricoDeNotificaçãoPTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) | Classe que armazena um log de objetos de notificação [ItemHistóricoNotificaçãoPTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) objetos que fornecem acesso a uma lista de histórico de eventos de notificação. Ou seja, mantém uma lista de elementos, cada elemento contendo uma instância separada do [PTNotification](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotification.html) |
| [ItemHistóricoNotificaçãoPTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistoryItem.html) | Classe que define uma entrada na lista circular em [HistóricoDeNotificaçãoPTN](https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTNotificationHistory.html) e mantém a notificação e seu carimbo de data e hora. |
