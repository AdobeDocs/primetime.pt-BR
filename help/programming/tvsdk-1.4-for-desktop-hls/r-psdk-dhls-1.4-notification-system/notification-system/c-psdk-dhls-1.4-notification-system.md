---
description: Os objetos MediaPlayerNotification fornecem informações sobre as alterações no status, nos avisos e nos erros do player. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.
title: Notificações para status, atividade, erros e registro do player
exl-id: cce634aa-5394-46c0-a031-70d6fc1b754b
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 0%

---

# Visão geral {#notifications-for-player-status-activity-errors-and-logging-overview}

Os objetos MediaPlayerNotification fornecem informações sobre as alterações no status, nos avisos e nos erros do player. Erros que interrompem a reprodução do vídeo também causam uma alteração no status do reprodutor.

Seu aplicativo pode recuperar a notificação e as informações de status. Você também pode criar um sistema de registro para diagnóstico e validação usando as informações de notificação.

Você implementa ouvintes de eventos para capturar e responder a eventos. Muitos eventos fornecem `MediaPlayerNotification` notificações de status.
