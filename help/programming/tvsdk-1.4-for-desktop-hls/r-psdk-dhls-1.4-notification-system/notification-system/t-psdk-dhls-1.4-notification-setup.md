---
description: Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.
title: Configurar seu sistema de notificação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '118'
ht-degree: 0%

---


# Configurar seu sistema de notificação{#set-up-your-notification-system}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.

O núcleo do sistema de notificação do Player do Primetime é a classe Notification , que representa uma notificação independente.

A classe NotificationHistory fornece um mecanismo para acumular notificações. Ele armazena um log de objetos de notificação ( `NotificationHistoryItem`) que representa uma coleção de Notificações.

Para receber notificações:

* Acompanhamento das notificações
* Adicionar notificações ao histórico de notificações

1. Analise as alterações de estado.
1. Implemente o ouvinte de evento `MediaPlayer.StatusChangeEvent.STATUS_CHANGED`.
1. O TVSDK transmite uma instância `MediaPlayer.StatusChangeEvent` para o ouvinte do evento, que contém dois parâmetros:

   * O novo estado ( `MediaPlayer.Status`)
   * Um objeto `MediaPlayerNotification`

