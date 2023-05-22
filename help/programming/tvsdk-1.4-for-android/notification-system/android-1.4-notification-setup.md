---
description: Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.
title: Configurar seu sistema de notificação
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 0%

---


# Configurar seu sistema de notificação{#set-up-your-notification-system}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.

O núcleo do sistema de notificação do Primetime Player é o `Notification` classe, que representa uma notificação independente.

A variável `NotificationHistory` A classe fornece um mecanismo para acumular notificações. Ele armazena um log de objetos de notificação (NotificationHistoryItem) que representa uma coleção de Notificações.

Para receber notificações:

* Acompanhar notificações
* Adicionar notificações ao histórico de notificações

1. Analise as alterações de estado.
1. Implementar o `MediaPlayer.PlaybackEventListener.onStateChanged` retorno de chamada.
1. O TVSDK passa dois parâmetros para o retorno de chamada:

   * O novo estado ( `MediaPlayer.PlayerState`)
   * A `MediaPlayerNotification` objeto

