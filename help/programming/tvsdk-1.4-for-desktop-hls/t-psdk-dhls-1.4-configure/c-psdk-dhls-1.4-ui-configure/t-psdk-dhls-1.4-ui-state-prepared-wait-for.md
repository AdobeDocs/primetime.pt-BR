---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.
title: Aguardar um estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Aguardar um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução para VOD (live and video on demand). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player. Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.

O reprodutor passa por vários status. Aguardar o reprodutor estar no status correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no status exigido, muitos métodos de reprodutor acionam `IllegalStateException`.

O status necessário geralmente é PREPARADO.

1. Para confirmar que o status é PREPARADO:

   Quando o reprodutor estiver inicializando, aguarde o TVSDK chamar o retorno de chamada para o `MediaPlayerStatusChangeEvent.STATUS_CHANGED` evento com status PREPARADO.

   Para verificar se o status atual da `MediaPlayer` objeto é pelo menos PREPARADO.

   ```
   function getstatus():String;
   ```
