---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.
title: Aguardar um status válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Aguardar um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução para VOD (live and video on demand). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.

Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.

Aguardar o reprodutor estar no status correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no status exigido, muitos métodos de reprodutor acionam `MediaPlayerException`.

O status necessário geralmente é PREPARADO. Quando isso ocorre, a rotina de retorno de chamada para `StatusChangeEventListener.onStatusChanged()` é executado.

1. Para confirmar que o status é `PREPARED`, verificar `MediaPlayer.MediaPlayerStatus`.
