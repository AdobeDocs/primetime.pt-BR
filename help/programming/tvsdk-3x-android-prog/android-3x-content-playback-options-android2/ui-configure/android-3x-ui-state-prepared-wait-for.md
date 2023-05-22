---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.
title: Aguardar um status válido
exl-id: bfd77163-7ca8-41e1-8b97-2d6a765f5ccd
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Aguardar um status válido {#wait-for-a-valid-status}

Com o TVSDK, você pode controlar a experiência básica de reprodução para VOD (live and video on demand). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.

Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.

Aguardar o reprodutor estar no status correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no status exigido, muitos métodos de reprodutor acionam `MediaPlayerException`.

O status necessário geralmente é PREPARADO. Quando isso ocorre, a rotina de retorno de chamada para `StatusChangeEventListener.onStatusChanged()` é executado.

Para confirmar que o status é `PREPARED`, verificar `MediaPlayer.MediaPlayerStatus`.
