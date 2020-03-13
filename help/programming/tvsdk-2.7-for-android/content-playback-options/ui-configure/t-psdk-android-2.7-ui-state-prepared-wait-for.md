---
description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-title: Aguarde um status válido
title: Aguarde um status válido
uuid: ffa63ad6-84d3-4eb2-aa99-026418d86528
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# Aguardar um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução de vídeo e ao vivo sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.

Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.

Aguardar o status correto do player garante que o recurso de mídia tenha sido carregado com êxito. Se o player não tiver pelo menos o status necessário, muitos métodos do player serão lançados `MediaPlayerException`.

O status necessário geralmente é PREPARADO. Quando isso ocorre, a rotina de retorno de chamada para `StatusChangeEventListener.onStatusChanged()` é executada.

1. Para confirmar que o status está `PREPARED`, verifique `MediaPlayer.MediaPlayerStatus`.
