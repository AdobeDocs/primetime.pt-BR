---
description: Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.
seo-description: Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.
seo-title: Configurar seu sistema de notificação
title: Configurar seu sistema de notificação
uuid: caa6a306-dea9-45ee-b0b3-569b5f2527a1
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 0%

---


# Configurar seu sistema de notificação{#set-up-your-notification-system}

Você pode acompanhar as notificações e adicionar suas próprias notificações ao histórico de notificações.

O núcleo do sistema de notificação do Primetime Player é a classe `Notification`, que representa uma notificação independente.

A classe `NotificationHistory` fornece um mecanismo para acumular notificações. Ele armazena um log de objetos de notificação (NotificationHistoryItem) que representa uma coleção de Notificações.

Para receber notificações:

* Escutar notificações
* Adicionar notificações ao histórico de notificações

1. Analise as mudanças de estado.
1. Implemente o retorno de chamada `MediaPlayer.PlaybackEventListener.onStateChanged`.
1. O TVSDK passa dois parâmetros para o retorno de chamada:

   * O novo estado ( `MediaPlayer.PlayerState`)
   * Um objeto `MediaPlayerNotification`

