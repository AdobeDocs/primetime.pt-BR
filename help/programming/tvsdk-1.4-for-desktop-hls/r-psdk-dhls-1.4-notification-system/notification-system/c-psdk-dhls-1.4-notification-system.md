---
description: Os objetos MediaPlayerNotification fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.
seo-description: Os objetos MediaPlayerNotification fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.
seo-title: Notificações de status, atividade, erros e registro do player
title: Notificações de status, atividade, erros e registro do player
uuid: 7ce5bed0-f312-437e-a82f-b1d4a8e1926c
translation-type: tm+mt
source-git-commit: adef0bbd52ba043f625f38db69366c6d873c586d

---


# Visão geral {#notifications-for-player-status-activity-errors-and-logging-overview}

Os objetos MediaPlayerNotification fornecem informações sobre alterações no status do player, avisos e erros. Os erros que param a reprodução do vídeo também causam uma alteração no status do player.

Seu aplicativo pode recuperar as informações de notificação e status. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem notificações `MediaPlayerNotification` de status.