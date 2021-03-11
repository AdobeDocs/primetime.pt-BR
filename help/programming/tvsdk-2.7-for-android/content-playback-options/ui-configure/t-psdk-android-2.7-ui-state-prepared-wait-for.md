---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um status válido.
title: Aguardar um status válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---


# Aguarde um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução de vídeo ao vivo e sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do reprodutor que você pode usar para configurar a interface do usuário do reprodutor.

Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um status válido.

Aguardar o status correto do reprodutor garante que ele tenha sido carregado com êxito. Se o reprodutor não tiver pelo menos o status necessário, muitos métodos do reprodutor exibirão `MediaPlayerException`.

O status necessário geralmente é PREPARADO. Quando isso ocorre, a rotina de retorno de chamada para `StatusChangeEventListener.onStatusChanged()` é executada.

1. Para confirmar que o status é `PREPARED`, marque `MediaPlayer.MediaPlayerStatus`.
