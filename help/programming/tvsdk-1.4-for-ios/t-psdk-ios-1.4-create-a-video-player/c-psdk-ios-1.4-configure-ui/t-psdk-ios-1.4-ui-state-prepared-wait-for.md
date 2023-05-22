---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.
title: Aguardar um estado válido
exl-id: 150b37b8-c36d-4143-bead-ddc601bba6fe
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---

# Aguardar um estado válido{#wait-for-a-valid-state}

Antes de usar a maioria dos métodos do reprodutor TVSDK, ele deve estar em um status válido.

O reprodutor passa por vários status. Aguardar o reprodutor estar no status correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no status exigido, muitos métodos de reprodutor acionam `IllegalStateException`.

Normalmente, o status necessário é `PTMediaPlayerStatusReady`.
