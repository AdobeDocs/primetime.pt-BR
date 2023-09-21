---
description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.
title: Classes de notificação
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Classes de notificação{#notification-classes}

Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.

Pacote: [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html)  Pacote: [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| Nome da classe | Descrição |
|---|---|
| MediaPlayerNotification. [Erro](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | Classe que descreve a notificação para um erro que faz com que o reprodutor pare de ser reproduzido. Este é um [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) do tipo de notificação ERRO. |
| MediaPlayerNotification. [Informações](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | Classe que descreve uma notificação informativa. Este é um [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) do tipo de notificação INFO. |
| MediaPlayerNotification. [Aviso](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | Classe que descreve uma notificação de aviso. Este é um [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) do tipo de notificação AVISO. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | Classe que fornece mensagens informativas, avisos e erros. Encapsula a representação do objeto de um único evento de notificação em [HistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | Retorna a descrição associada ao código de notificação fornecido. |
| [HistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | Classe que armazena um log de objetos de notificação. Uma lista circular de [HistóricoNotificação.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) objetos que fornecem acesso a uma lista de histórico de eventos de notificação. Ou seja, mantém uma lista de elementos, cada elemento contendo uma instância separada do [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) classe. (Em [session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) pacote.) |
| HistóricoNotificação. [Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | Classe que define uma entrada na lista circular em [HistóricoNotificação](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) e mantém a notificação e seu carimbo de data e hora. |
| MediaPlayerNotification. [EntryType](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | Classe que contém os tipos de notificações aceitos. |
