---
description: Os objetos MediaPlayerNotification fornecem informações sobre alterações no status do player, avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.
title: Notificações para status, atividade, erros e registro do player
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---


# Visão geral {#notifications-for-player-status-activity-errors-and-logging-overview}

Os objetos MediaPlayerNotification fornecem informações sobre alterações no status do player, avisos e erros. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.

Seu aplicativo pode recuperar a notificação e as informações de status. Você também pode criar um sistema de registro para diagnósticos e validação usando as informações de notificação.

Você implementa ouvintes de eventos para capturar e responder aos eventos. Muitos eventos fornecem notificações de status `MediaPlayerNotification`.