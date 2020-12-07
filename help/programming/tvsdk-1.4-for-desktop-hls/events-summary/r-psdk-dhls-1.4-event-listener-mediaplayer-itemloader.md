---
description: O TVSDK despacha eventos de item do player de mídia em resposta ao carregamento de um item de mídia.
seo-description: O TVSDK despacha eventos de item do player de mídia em resposta ao carregamento de um item de mídia.
seo-title: Eventos do carregador
title: Eventos do carregador
uuid: 0ad37715-14b1-457c-892f-0db0d6220f0c
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb
workflow-type: tm+mt
source-wordcount: '137'
ht-degree: 0%

---


# Eventos do carregador{#loader-events}

O TVSDK despacha eventos de item do player de mídia em resposta ao carregamento de um item de mídia.

Esses eventos fornecem um fluxo de trabalho alternativo. Não é necessário implementar essa interface ao criar um `MediaPlayer`. Use-o quando quiser ter um `MediaPlayerItemLoader`.

Para ser notificado sobre eventos relacionados ao carregamento de um recurso de player de mídia, registre os ouvintes dos seguintes eventos com o objeto `MediaPlayerItemLoader`.

| Evento | Significado |
|---|---|
| MediaPlayerItemLoader.[completed](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | O carregamento do recurso de mídia foi concluído com êxito. |
| MediaPlayerItemLoader.[failed](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Ocorreu um problema com o carregamento de recursos de mídia. |