---
description: Antes de usar a maioria dos métodos do player TVSDK do navegador, o player deve estar em um estado válido.
title: Aguardar um estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---


# Aguarde um estado válido {#wait-for-a-valid-state}

Antes de usar a maioria dos métodos do player TVSDK do navegador, o player deve estar em um estado válido.

O reprodutor passa por vários estados. Aguardar o estado correto do reprodutor garante que este tenha sido carregado com êxito. Se o reprodutor não estiver no estado exigido, muitos métodos do reprodutor exibirão `IllegalStateException`.

O estado necessário geralmente é PREPARADO.

1. Para confirmar que o estado é PREPARADO:

   Quando o reprodutor estiver inicializando, aguarde o Browser TVSDK despachar o evento `AdobePSDK.MediaPlayerStatusChangeEvent` com um `event.status` de `MediaPlayerStatus.PREPARED`.

   Para verificar se o estado atual do objeto MediaPlayer é, pelo menos, PREPARADO.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

