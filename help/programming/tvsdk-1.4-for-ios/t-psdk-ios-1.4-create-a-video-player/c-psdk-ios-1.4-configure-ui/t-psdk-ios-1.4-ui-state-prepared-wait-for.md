---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.
title: Aguardar um estado válido
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Aguardar um estado válido{#wait-for-a-valid-state}

Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.

O reprodutor passa por vários status. Aguardar o reprodutor estar no status correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no status exigido, muitos métodos de reprodutor acionam `IllegalStateException`.

Normalmente, o status necessário é `PTMediaPlayerStatusReady`.
