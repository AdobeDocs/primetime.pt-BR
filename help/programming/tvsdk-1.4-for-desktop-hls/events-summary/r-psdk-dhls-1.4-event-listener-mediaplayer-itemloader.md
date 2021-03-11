---
description: O TVSDK envia eventos de item do reprodutor de mídia em resposta ao carregamento de um item de mídia.
title: Eventos de carregador
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---


# Eventos de carregador{#loader-events}

O TVSDK envia eventos de item do reprodutor de mídia em resposta ao carregamento de um item de mídia.

Esses eventos fornecem um workflow alternativo. Não é necessário implementar essa interface ao criar um `MediaPlayer`. Use essa opção quando quiser ter um `MediaPlayerItemLoader`.

Para ser notificado sobre eventos relacionados ao carregamento de um recurso do reprodutor de mídia, registre os ouvintes dos seguintes eventos no objeto `MediaPlayerItemLoader` .

| Evento | Significado |
|---|---|
| MediaPlayerItemLoader.[concluído](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | Carregamento do recurso de mídia concluído com êxito. |
| MediaPlayerItemLoader.[falha](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Ocorreu um problema com o carregamento de recursos de mídia. |