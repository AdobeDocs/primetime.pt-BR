---
description: Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.
seo-description: Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.
seo-title: Configurar seu sistema de notificação
title: Configurar seu sistema de notificação
uuid: 2d1876c7-4ce6-491c-880b-dd94697d4feb
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---


# Configurar seu sistema de notificação{#set-up-your-notification-system}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.

O núcleo do sistema de notificação do Primetime Player é a classe Notification, que representa uma notificação independente.

A classe NotificationHistory fornece um mecanismo para acumular notificações. Ele armazena um log de objetos de notificação ( `NotificationHistoryItem`) que representa uma coleção de Notificações.

Para receber notificações:

* Escutar notificações
* Adicionar notificações ao histórico de notificações

1. Analise as mudanças de estado.
1. Implemente o ouvinte do evento `MediaPlayer.StatusChangeEvent.STATUS_CHANGED`.
1. O TVSDK transmite uma instância `MediaPlayer.StatusChangeEvent` para o ouvinte do evento, que contém dois parâmetros:

   * O novo estado ( `MediaPlayer.Status`)
   * Um objeto `MediaPlayerNotification`

