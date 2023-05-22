---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.
title: Aguardar um status válido
exl-id: fddb6696-9226-408d-be3c-58d4ce7db55d
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
