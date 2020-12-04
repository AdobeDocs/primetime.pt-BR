---
description: Antes de usar a maioria dos métodos do player TVSDK do navegador, o player deve estar em um estado válido.
seo-description: Antes de usar a maioria dos métodos do player TVSDK do navegador, o player deve estar em um estado válido.
seo-title: Aguardar um estado válido
title: Aguardar um estado válido
uuid: 0add29a8-fbd8-483a-8c99-e4bc6de9e3d3
translation-type: tm+mt
source-git-commit: 592245f5a7186d18dabbb5a98a468cbed7354aed
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---


# Aguarde um estado válido {#wait-for-a-valid-state}

Antes de usar a maioria dos métodos do player TVSDK do navegador, o player deve estar em um estado válido.

O jogador passa por vários estados. Aguardar o player no estado correto garante que o recurso de mídia tenha sido carregado com êxito. Se o player não estiver no estado necessário, muitos métodos do player lançam `IllegalStateException`.

O estado necessário geralmente é PREPARADO.

1. Para confirmar que o estado está PREPARADO:

   Quando o player estiver inicializando, aguarde o TVSDK do navegador despachar o evento `AdobePSDK.MediaPlayerStatusChangeEvent` com um `event.status` de `MediaPlayerStatus.PREPARED`.

   Para verificar se o estado atual do objeto MediaPlayer é pelo menos PREPARADO.

   ```
   <readonly> status :AdobePSDK.MediaPlayerStatus
   ```

