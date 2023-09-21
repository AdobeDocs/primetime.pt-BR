---
description: MediaPlayerNotification fornece informações relacionadas ao status do player.
title: Conteúdo da notificação
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---

# Conteúdo da notificação{#notification-content}

MediaPlayerNotification fornece informações relacionadas ao status do player.

O TVSDK fornece uma lista cronológica de `MediaPlayerNotification` notificações. Cada notificação contém as seguintes informações:

* Carimbo de data/hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * digite INFO, WARN ou ERROR
   * `code`: uma representação numérica da notificação.
   * `name`: uma descrição legível da notificação, como SEEK_ERROR
   * `metadata`: Pares de chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` O fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outra `MediaPlayerNotification` objeto que afeta diretamente esta notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las a um servidor remoto para registro e representação gráfica.
