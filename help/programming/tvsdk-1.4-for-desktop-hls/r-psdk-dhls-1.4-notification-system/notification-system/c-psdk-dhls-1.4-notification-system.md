---
description: Os objetos MediaPlayerNotification fornecem informações sobre as alterações no status, nos avisos e nos erros do player. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.
title: Notificações para status, atividade, erros e registro do player
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Visão geral {#notifications-for-player-status-activity-errors-and-logging-overview}

Os objetos MediaPlayerNotification fornecem informações sobre as alterações no status, nos avisos e nos erros do player. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.

Seu aplicativo pode recuperar a notificação e as informações de status. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem `MediaPlayerNotification` notificações de status.
