---
description: Antes de usar a maioria dos métodos de player TVSDK do navegador, o player deve estar em um estado válido.
title: Aguardar um estado válido
exl-id: 14f6a5db-4f81-448b-b291-487569a7bc4e
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
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
