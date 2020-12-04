---
description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-title: Aguardar um estado válido
title: Aguardar um estado válido
uuid: 918ab021-3685-424a-b84e-683da0357724
translation-type: tm+mt
source-git-commit: 8ff38bdc1a7ff9732f7f1fae37f64d0e1113ff40
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---


# Aguarde um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução para vídeo ao vivo e sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player. Antes de usar a maioria dos métodos do player do TVSDK, o player deve estar em um status válido.

O player se move por vários status. Aguardar o status correto do player garante que o recurso de mídia tenha sido carregado com êxito. Se o player não tiver pelo menos o status necessário, muitos métodos do player lançarão `IllegalStateException`.

O status necessário geralmente é PREPARADO.

1. Para confirmar que o status é PREPARADO:

   Quando o player estiver inicializando, aguarde o TVSDK chamar o retorno de chamada para o evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` com o status PREPARED.

   Para verificar se o status atual do objeto `MediaPlayer` é pelo menos PREPARADO.

   ```
   function getstatus():String;
   ```
