---
description: MediaPlayerNotification fornece informações relacionadas ao status do player.
seo-description: MediaPlayerNotification fornece informações relacionadas ao status do player.
seo-title: Conteúdo da notificação
title: Conteúdo da notificação
uuid: c2321a49-1b60-4e44-b8e2-a023b764d779
translation-type: tm+mt
source-git-commit: 7e8df034035fe465fbe403949ef828e7811ced2e
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Conteúdo da notificação{#notification-content}

MediaPlayerNotification fornece informações relacionadas ao status do player.

O TVSDK fornece uma lista cronológica de `MediaPlayerNotification` notificações. Cada notificação contém as seguintes informações:

* Carimbo de data e hora
* Metadados de diagnóstico que consistem nos seguintes elementos:

   * digite INFO, AVISO ou ERRO
   * `code`: Uma representação numérica da notificação.
   * `name`: Uma descrição legível pela pessoa da notificação, como SEEK_ERROR
   * `metadata`: Pares chave/valor que contêm informações relevantes sobre a notificação. Por exemplo, uma chave chamada `URL` fornece um valor que é um URL relacionado à notificação.

   * `innerNotification`: Uma referência a outro  `MediaPlayerNotification` objeto que afeta diretamente essa notificação.

Você pode armazenar essas informações localmente para análise posterior ou enviá-las para um servidor remoto para registro e representação gráfica.
