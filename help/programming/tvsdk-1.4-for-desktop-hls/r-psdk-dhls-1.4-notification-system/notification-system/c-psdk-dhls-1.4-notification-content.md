---
description: MediaPlayerNotification fornece informações relacionadas ao status do player.
title: Conteúdo de notificação
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '125'
ht-degree: 0%

---


# Conteúdo de notificação{#notification-content}

MediaPlayerNotification fornece informações relacionadas ao status do player.

O TVSDK fornece uma lista cronológica de notificações `MediaPlayerNotification`. Cada notificação contém as seguintes informações:

* Carimbo de data/hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * digitar INFO, AVISO ou ERRO
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível da notificação, como SEEK_ERROR
   * `metadata`: Pares de chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro  `MediaPlayerNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las a um servidor remoto para registro e representação gráfica.
