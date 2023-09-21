---
description: Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.
title: Configurar seu sistema de notificação
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---

# Configurar seu sistema de notificação{#set-up-your-notification-system}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.

O núcleo do sistema de notificação do Primetime Player é a classe Notification, que representa uma notificação independente.

A classe NotificationHistory fornece um mecanismo para acumular notificações. Ele armazena um log de notificação ( `NotificationHistoryItem`) que representa uma coleção de Notificações.

Para receber notificações:

* Acompanhar notificações
* Adicionar notificações ao histórico de notificações

1. Analise as alterações de estado.
1. Implementar o `MediaPlayer.StatusChangeEvent.STATUS_CHANGED` ouvinte de eventos.
1. O TVSDK passa um `MediaPlayer.StatusChangeEvent` ao ouvinte de eventos, que contém dois parâmetros:

   * O novo estado ( `MediaPlayer.Status`)
   * A `MediaPlayerNotification` objeto
