---
description: O TVSDK despacha eventos de itens de reprodutor de mídia em resposta ao carregamento de um item de mídia.
title: Eventos carregadores
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 0%

---

# Eventos carregadores{#loader-events}

O TVSDK despacha eventos de itens de reprodutor de mídia em resposta ao carregamento de um item de mídia.

Esses eventos fornecem um fluxo de trabalho alternativo. Não é necessário implementar essa interface ao criar uma `MediaPlayer`. Use isso quando quiser ter um `MediaPlayerItemLoader`.

Para ser notificado sobre eventos relacionados ao carregamento de um recurso de reprodutor de mídia, registre os ouvintes dos seguintes eventos na `MediaPlayerItemLoader` objeto.

| Evento | Significado |
|---|---|
| MediaPlayerItemLoader.[concluído](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:completed) | O carregamento do recurso de mídia foi concluído com êxito. |
| MediaPlayerItemLoader.[falhou](https://help.adobe.com/en_US/primetime/api/psdk/asdoc-dhls_1.4/com/adobe/mediacore/MediaPlayerItemLoader.html#event:failed) | Ocorreu um problema com o carregamento do recurso de mídia. |
