---
description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-title: Aguardar um estado válido
title: Aguardar um estado válido
uuid: e13201d7-b217-4d01-bdb7-a71855e3500e
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '113'
ht-degree: 0%

---


# Aguarde um estado válido{#wait-for-a-valid-state}

Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.

O player se move por vários status. Aguardar o status correto do player garante que o recurso de mídia tenha sido carregado com êxito. Se o player não tiver pelo menos o status necessário, muitos métodos do player lançarão `IllegalStateException`.

O status necessário geralmente é `PTMediaPlayerStatusReady`.
