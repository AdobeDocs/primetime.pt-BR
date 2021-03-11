---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um status válido.
title: Aguardar um estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---


# Aguarde um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução de vídeo sob demanda (VOD). O TVSDK fornece métodos e propriedades na instância do reprodutor que você pode usar para configurar a interface do usuário do reprodutor. Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um status válido.

O reprodutor passa por vários status. Aguardar o status correto do reprodutor garante que ele tenha sido carregado com êxito. Se o reprodutor não estiver no status mínimo necessário, muitos métodos do reprodutor exibirão `IllegalStateException`.

O status necessário geralmente é PREPARADO.

1. Para confirmar que o status é PREPARADO:

   Quando o reprodutor estiver inicializando, aguarde o TVSDK chamar o retorno de chamada para o evento `MediaPlayerStatusChangeEvent.STATUS_CHANGED` com o status PREPARED.

   Para verificar se o status atual do objeto `MediaPlayer` é pelo menos PREPARED.

   ```
   function getstatus():String;
   ```
