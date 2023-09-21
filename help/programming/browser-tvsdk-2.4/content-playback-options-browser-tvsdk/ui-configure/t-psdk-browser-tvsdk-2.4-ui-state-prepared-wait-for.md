---
description: Antes de usar a maioria dos métodos de player TVSDK do navegador, o player deve estar em um estado válido.
title: Aguardar um estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 0%

---

# Aguardar um estado válido {#wait-for-a-valid-state}

Antes de usar a maioria dos métodos de player TVSDK do navegador, o player deve estar em um estado válido.

O reprodutor passa por vários estados. Aguardar o reprodutor para estar no estado correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no estado obrigatório, muitos métodos de reprodutor acionarão `IllegalStateException`.

O estado obrigatório é geralmente PREPARADO.

1. Para confirmar que o estado é PREPARADO:

   Quando o reprodutor estiver inicializando, aguarde o TVSDK do navegador despachar o `AdobePSDK.MediaPlayerStatusChangeEvent` evento com um `event.status` de `MediaPlayerStatus.PREPARED`.

   Para verificar se o estado atual do objeto MediaPlayer é pelo menos PREPARADO.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```
