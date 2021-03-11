---
description: Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um status válido.
title: Aguardar um estado válido
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '90'
ht-degree: 0%

---


# Aguarde um estado válido{#wait-for-a-valid-state}

Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um status válido.

O reprodutor passa por vários status. Aguardar o status correto do reprodutor garante que ele tenha sido carregado com êxito. Se o reprodutor não tiver pelo menos o status necessário, muitos métodos do reprodutor exibirão `IllegalStateException`.

O status necessário geralmente é `PTMediaPlayerStatusReady`.
