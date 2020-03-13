---
description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.
seo-description: Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.
seo-title: Classes de notificação
title: Classes de notificação
uuid: e231a2d0-6190-4251-87db-ca46d2aee60d
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Classes de notificação{#notification-classes}

Essas classes descrevem mensagens sobre erros, avisos e algumas atividades que o TVSDK emite para fins de registro e depuração.

Pacote: Pacote [com.adobe.mediacore](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/package-summary.html) : [com.adobe.mediacore.session](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html)

| Nome da classe | Descrição |
|---|---|
| MediaPlayerNotification. [Erro](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Error.html) | Classe que descreve a notificação de um erro que faz com que o player pare a reprodução. Esta é uma [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) do tipo de notificação ERROR. |
| MediaPlayerNotification. [Informações](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Info.html) | Classe que descreve uma notificação informativa. Esta é uma [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) do tipo de notificação INFO. |
| MediaPlayerNotification. [Aviso](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.Warning.html) | Classe que descreve uma notificação de aviso. Esta é uma [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) do tipo de notificação AVISO. |
| [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) | Classe que fornece mensagens informativas, avisos e erros. Encapsula a representação de objeto de um único evento de notificação em [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html). |
| MediaPlayerNotification. [NotificationCode](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.NotificationCode.html) | Retorna a descrição associada ao código de notificação fornecido. |
| [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) | Classe que armazena um log de objetos de notificação. Uma lista circular de objetos [NotificationHistory.Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) que fornece acesso a uma lista de histórico de eventos de notificação. Ou seja, ele mantém uma lista de elementos, cada elemento contendo uma instância separada da classe [MediaPlayerNotification](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.html) . (No pacote de [sessão](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/package-summary.html) .) |
| NotificationHistory. [Item](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.Item.html) | Classe que define uma entrada na lista circular em [NotificationHistory](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/session/NotificationHistory.html) e armazena a notificação e seu carimbo de data e hora. |
| MediaPlayerNotification. [TipoEntrada](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_1.4/com/adobe/mediacore/MediaPlayerNotification.EntryType.html) | Classe que contém os tipos de notificações suportados. |