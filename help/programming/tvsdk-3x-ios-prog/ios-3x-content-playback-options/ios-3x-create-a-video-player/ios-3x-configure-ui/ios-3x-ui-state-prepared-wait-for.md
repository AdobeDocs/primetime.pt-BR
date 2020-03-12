---
description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-description: Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.
seo-title: Aguardar um estado válido
title: Aguardar um estado válido
uuid: ad9df366-c443-4e6b-a7ab-658d5691eb94
translation-type: tm+mt
source-git-commit: a63768e51c911914a6ba9d884e2587fa34939f9d

---


# Aguardar um estado válido {#wait-for-a-valid-state}

Antes de usar a maioria dos métodos do player TVSDK, o player deve estar em um status válido.

O player se move por vários status. Aguardar o status correto do player garante que o recurso de mídia tenha sido carregado com êxito. Se o player não tiver pelo menos o status necessário, muitos métodos do player serão lançados `IllegalStateException`.

O status necessário é geralmente `PTMediaPlayerStatusReady`.