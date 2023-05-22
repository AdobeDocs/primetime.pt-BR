---
description: Com o TVSDK, você pode controlar a experiência básica de reprodução para VOD (live and video on demand). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.
title: Aguardar um estado válido
exl-id: ab9da066-429f-44ca-b2e7-2bde9e5c0f90
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 0%

---

# Aguardar um estado válido {#wait-for-a-valid-state}

Com o TVSDK, você pode controlar a experiência básica de reprodução para VOD (live and video on demand). O TVSDK fornece métodos e propriedades na instância do player que você pode usar para configurar a interface do usuário do player.

Antes de usar a maioria dos métodos do reprodutor TVSDK, o reprodutor deve estar em um estado válido.
O reprodutor passa por vários estados. Aguardar o reprodutor para estar no estado correto garante que o recurso de mídia foi carregado com êxito. Se o reprodutor não estiver pelo menos no estado obrigatório, muitos métodos de reprodutor acionarão `IllegalStateException`.

O estado obrigatório é geralmente PREPARADO.
